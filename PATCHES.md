# Local compatibility patches

## Scope

只对新安装技能做了三处兼容修复，未更改需求访谈、工作流或设计策略。
补丁为 `patches/windows-codex.patch`；基准文件与适配文件的 LF 规范化 SHA-256 在 `patches/checksums.json`。
新机器先比对基准 SHA-256。若不一致，检查上游是否已经修复；不要强行套用过期补丁。

## ui-ux-pro-max / SKILL.md

上游示例通过 `${CLAUDE_PLUGIN_ROOT}/.claude/skills/ui-ux-pro-max` 查找脚本。独立安装到 Codex 时该变量不适用。
改为 `{baseDir}`，并说明它是当前 SKILL.md 所在目录的绝对路径。只替换路径约定。
这不表示 Claude Code 自带插件应修改；仅针对独立 skill 安装布局。

## baoyu-format-markdown / scripts/main.ts

上游直接拼接 `file://${process.argv[1]}` 判断 CLI 入口，Windows 路径与 file URL 不一致，导致退出码 0 但没有执行。
改用 Node `pathToFileURL(resolve(process.argv[1]))`。已复现原失败并验证 --help 和实际格式化。

## baoyu-format-markdown / scripts/autocorrect.ts

Windows 下直接 spawn npx.cmd 未实际执行，返回结果 spacingApplied=false。
在 Windows + Bun 下用 `process.execPath` 启动 `bun x autocorrect-node --fix <file>`，通过 argv 数组传参。
其他平台使用 npx。已用临时中文文件验证 spacingApplied=true 且文本出现正确中英间距。

## Applying

在目标全局技能目录下先预检，再应用：

```sh
git apply --check /path/to/ai-dev-environment/patches/windows-codex.patch
git apply /path/to/ai-dev-environment/patches/windows-codex.patch
```

仅在目标目录是预期技能根目录、基准匹配时运行。若宿主不允许在非 Git 目录 apply，先在单独的临时技能目录应用，再复制已验证文件。
也可以由 AI 按上述三项做等价修改并执行同样验证。更新技能后重新核对，避免覆盖已修复的上游。
