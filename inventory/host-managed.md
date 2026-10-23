# Host-managed inventory

这些条目来自当前宿主目录或本会话暴露的能力。目录存在不等于插件已安装、已连接或已授权。
它们不是本清单的独立 GitHub 技能安装目标；换机后优先使用宿主官方安装和设置界面恢复。

## User .agents/skills (observed)

- `automate`
- `autopilot`
- `canvas`
- `create-hook`
- `create-rule`
- `create-skill`
- `create-subagent`
- `goal`
- `loop`
- `migrate-to-skills`
- `new-repo`
- `onboard`
- `origin`
- `rename-chat`
- `review`
- `review-bugbot`
- `review-security`
- `sdk`
- `share`
- `shell`
- `split-to-prs`
- `statusline`
- `update-cli-config`
- `update-cursor-settings`
- `visualize`

## Codex system skills (observed)

- `imagegen`
- `openai-docs`
- `review-agent`
- `skill-creator`
- `skill-installer`

## Session-provided plugin/runtime capabilities

- Context7：已确认连接；换机通过插件界面重新安装/登录，不复制 OAuth token。
- GitHub：已确认连接；新机器需重新授权。建库如无连接器接口，使用官方网页或已登录的 CLI。
- Pages、Plugin Creator、Shopify、Sites、Work Pets：本会话提供相关工具，不推断账号已登录或业务服务已授权。
- Computer Use、Visualize、Documents、PDF、Presentations、Spreadsheets、Template Creator、Code Review、Codex App Tools：宿主提供或管理，版本跟随应用；使用官方插件/宿主分发恢复。

## Existing local MCP configuration

- `serial-studio`：本次已配置，见主文档。
- `logic2`：本次已配置，见主文档。
- `node_repl`：宿主运行时，应用管理；不要复制带版本号的绝对路径。
- `marker-pdf`：原有本地 Python 服务；未核实可独立下载的上游来源，按用户要求不纳入自动恢复。
