# AI Development Environment

## 给恢复环境的 AI

这是嵌入式 MCU、Python 上位机与技术报告的个人环境清单。目标是复用能力与约定，不复制旧电脑的整个配置目录。

1. 先读本文；再按任务读取 `skills.json`、`ENVIRONMENT.md` 或 `PATCHES.md`。
2. 恢复用户全局技能；目标目录由当前 agent 的官方文档和现有配置决定，不假设所有工具共用目录。
3. 优先使用清单中上游官方仓库/作者仓库的原始技能；需要本地适配的只有 `ui-ux-pro-max` 和 `baoyu-format-markdown`，见 PATCHES.md。
4. 不覆盖已有同名技能；先比较来源和差异。不要同时安装同一技能的独立版、符号链接版和插件捆绑版。
5. 本清单只授权环境恢复；固件烧录、Flash 擦除、设备写入、电机运动等操作按当前任务授权执行。
6. 缺少官方下载渠道、账号权限、硬件或许可时，记录为未恢复并继续其他项目；不要寻找非官方破解包。
7. 不提交凭据、OAuth token、SSH 私钥、实际业务固件、日志或完整的宿主 config.toml。

## 工作场景与约定

- MCU：STM32 / GD32 / LKS32；实体产品的按键、通信、灯、屏幕和电机功能。
- PC 工具：现有上位机采用 PyQt6；纯 Python CLI 项目继续保持 CLI，不自动引入 Qt。
- UI：沿用已选主题和已有设计系统；frontend-design 的探索建议应服从当前项目的既定主题。
- HTML 报告：明确单位、采样条件、硬件/固件版本、异常和结论；原始数据独立保留。
- Markdown：工程文档保留技术标题和内容语义。baoyu-format-markdown 偏文章排版，按任务决定是否使用 frontmatter、标题优化和摘要，不机械套用。
- skill 是方法与工具封装，不等于 MCU 编译器、驱动、仿真器或硬件。PC 测试不能替代外设和板上验证。

## 快速恢复

需要 Git、Python 3 和 Node.js/npm（使用 npx 时）。先检查当前机器已有工具。

对支持 Skills CLI 的 agent，可从以下单项安装示例开始：

```sh
npx skills add vercel-labs/skills --skill find-skills -g -y
npx skills add wshobson/agents --skill python-code-style python-testing-patterns -g -y
npx skills add anthropics/skills --skill frontend-design theme-factory -g -y
npx skills add nextlevelbuilder/ui-ux-pro-max-skill --skill ui-ux-pro-max -g -y
npx skills add jimliu/baoyu-skills --skill baoyu-format-markdown baoyu-markdown-to-html -g -y
```

以上命令跟随上游默认分支，适合快速获取新版，不代表历史逐字复原。CLI 可能询问目标 agent；检查当前 `npx skills --help`，只选择需要的宿主。

若要使用本文核对过来源的固定基线，逐条读取 `skills.json` 的 `repository`、`restore_ref` 和 `path`，通过宿主的 GitHub skill installer 安装。例如 Codex 自带安装器：

```sh
python <CODEX_SKILL_INSTALLER>/scripts/install-skill-from-github.py --repo anthropics/skills --ref dbd4588f9e1033efb41dad4bef2f7947c8993d44 --path skills/frontend-design skills/theme-factory --dest <TARGET_SKILLS_DIR> --method git
```

`<CODEX_SKILL_INSTALLER>` 是本机 skill-installer 的目录，不是固定用户名路径。其他 agent 可克隆指定提交，然后把每个 skill 目录及 scripts/references/data/assets 一起复制到该宿主支持的全局目录。不要只复制 SKILL.md。

本机原安装没有记录 Git commit。`restore_ref` 是整理时核对的上游提交基线，不冒充原安装版本。`installed_manifest_sha256` 是本机 SKILL.md 字节快照，只覆盖清单文件，不覆盖全部脚本。来源核对结果在 `inventory/source-verification.json`（如存在）。

## 可从上游恢复的全局技能

### superpowers

来源：[obra/superpowers](https://github.com/obra/superpowers)。需求澄清、计划、实现、调试、测试和验证流程。

- `brainstorming`
- `diagnosing-superpowers`
- `dispatching-parallel-agents`
- `executing-plans`
- `finishing-a-development-branch`
- `receiving-code-review`
- `requesting-code-review`
- `subagent-driven-development`
- `systematic-debugging`
- `test-driven-development`
- `using-git-worktrees`
- `using-superpowers`
- `verification-before-completion`
- `writing-plans`
- `writing-skills`

### requirements

来源：[mattpocock/skills](https://github.com/mattpocock/skills)。需求访谈与文档完善；grill-me / grill-with-docs 是显式入口，依赖 grilling / domain-modeling。

- `domain-modeling`
- `grill-me`
- `grill-with-docs`
- `grilling`

### discovery

来源：[vercel-labs/skills](https://github.com/vercel-labs/skills)。检索其他可安装技能。

- `find-skills`

### embedded

来源：[zhinkgit/embeddedskills](https://github.com/zhinkgit/embeddedskills)。嵌入式构建、烧录、调试与串口/CAN/网络操作；先核实后端工具、芯片和探针配置。

- `can`
- `eide`
- `gcc`
- `jlink`
- `keil`
- `net`
- `openocd`
- `probe-rs`
- `serial`
- `ssh`
- `terminal`
- `workflow`

### embedded-tests

来源：[easyzoom/aix-skills](https://github.com/easyzoom/aix-skills)。嵌入式 C 的 Unity / Ceedling / CMock 主机测试。

- `unity-ceedling-integration`

### python

来源：[wshobson/agents](https://github.com/wshobson/agents)。Python 风格规范与 pytest / Mock 测试。

- `python-code-style`
- `python-testing-patterns`

### visual

来源：[anthropics/skills](https://github.com/anthropics/skills)。HTML/UI 视觉设计和可复用主题。

- `frontend-design`
- `theme-factory`

### ui

来源：[nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)。布局、交互、可访问性、图表与设计系统检索。

- `ui-ux-pro-max`

### markdown

来源：[jimliu/baoyu-skills](https://github.com/jimliu/baoyu-skills)。中文 Markdown 排版和样式化 HTML 导出。

- `baoyu-format-markdown`
- `baoyu-markdown-to-html`

## 插件与 MCP

- **Context7**：公共库的版本文档与代码示例查询。通过宿主官方插件目录安装并登录。普通公共文档查询不需要把工作仓库交给 GitHub App。
- **GitHub**：查看仓库、Issue、PR 和 CI，以及在权限与 CLI 支持下提交变更。换机重新授权；连接器是否支持创建仓库以实际暴露能力为准。
- **Serial Studio MCP**：应用需先运行，API 仅绑定本机；通过上游 Python stdio 桥接连接。应用、桥接脚本和 Python 路径需要按环境修改。
- **Saleae Logic MCP**：运行支持 MCP 的 Logic 版本，服务 `http://127.0.0.1:10530`。本机用 `--mcp` 启动；硬件驱动与设备另装。

其他宿主管理条目单列在 [inventory/host-managed.md](inventory/host-managed.md)。缓存目录不作为连接成功的证据。

## 按环境修改

详见 [ENVIRONMENT.md](ENVIRONMENT.md)。最关键的变量是：全局 skill 目录、Python/Node 路径、编译器路径、MCU 型号、探针序列号、串口/CAN 接口、驱动、SSH Host 别名以及 MCP 应用启动方式。

可从 [mcp.codex.example.toml](mcp.codex.example.toml) 挑选段落合并到本机配置，不覆盖整个配置，不把示例占位符当作已安装路径。

## AI 上下文与缓存约定

- 本文保留稳定的任务入口、技能 ID 和章节顺序；机器路径、版本观察值和状态放在独立文件。
- 按需读取具体 skill；不要在每次任务中粘贴所有技能全文，也不要无理由安装全部宿主插件。
- 更新条目时修改必要字段；不要为了“优化提示词”反复重写总览、打乱字段或加入每次变化的时间戳。
- API 提示缓存依赖相同前缀及运行条件。稳定前缀有助于复用，但跨机器、跨模型、跨 agent 不承诺共享缓存；仓库是配置来源，不是缓存存储。不要为了凑缓存长度增加无关文本。
- 当前任务输入和机器检查结果放在稳定说明之后。宿主如何组装提示词、工具定义与技能元数据仍由宿主控制。

## 官方资料

- [Codex / ChatGPT skills](https://learn.chatgpt.com/docs/build-skills)
- [OpenAI prompt caching](https://developers.openai.com/api/docs/guides/prompt-caching)
- [Skills CLI](https://github.com/vercel-labs/skills)
- [Context7](https://github.com/upstash/context7)
- [Serial Studio](https://github.com/Serial-Studio/Serial-Studio)
- [Saleae Logic](https://www.saleae.com/downloads/)
- [LVGL PC simulator](https://github.com/lvgl/lv_port_pc_vscode)

本文与清单可以独立维护。第三方技能继续使用各自上游许可证；仓库只记录来源和本地小补丁，不重新授权第三方内容。
