# Environment adaptations

## Host and skill directories

- 当前参考环境：Windows / PowerShell / Codex，用户技能实际位于 `~/.codex/skills`。
- 新版 Codex 官方文档也说明用户级 `~/.agents/skills`；以目标安装版本的扫描规则为准。不要向两处各复制一份造成重复发现。
- Cursor、Claude Code 等工具按各自的官方全局目录或 CLI agent 选项恢复。SKILL.md 格式可复用，工具名、Shell 语法和权限流程未必通用。
- 系统技能、宿主插件、运行时通过官方安装器恢复，参见 inventory/host-managed.md；不要复制应用缓存中的带版本绝对路径。

## Embedded backends

- Keil：Windows，需单独安装和配置 UV4、许可及设备包。
- GCC：`arm-none-eabi-gcc` 是 MCU 交叉编译器；本机为了 PC 测试安装的主机 GCC 不能代替它。
- EIDE：安装官方扩展和构建工具，检查每个工程配置名和工具链路径。
- J-Link / OpenOCD / probe-rs：安装对应工具及驱动；按 MCU 型号、Flash 地址、接口速度、连接方式和探针选择配置。
- 串口：Windows COM 名与 Linux/macOS 设备名不同。CAN 适配器后端、驱动、波特率和 DBC 路径按机器/工程设置。
- SSH：仅保留 `~/.ssh/config` Host 别名设计，私钥与凭据单独配置，不进入仓库。

## PC test and simulation tools

这些是已有安装的版本观察值，不是对新电脑可用性的承诺。仅从对应上游官方下载；不可直接获取的商业工具可以跳过。

- Ruby 3.4.11、Ceedling 1.2.0、Unity 2.7.2、CMock 2.7.2：Unity/CMock 由 Ceedling 管理；先验证一个官方示例再接入实际工程。上游 https://github.com/ThrowTheSwitch/Ceedling 。
- 主机 GCC 16.2.0、CMake 4.4.4、Ninja 1.13.2：本机来自 RubyInstaller/MSYS2 与官方发行，平台不同时使用相应官方安装方式。
- LVGL 官方 PC 模拟器：源码 https://github.com/lvgl/lv_port_pc_vscode ，需递归子模块；本机 SDL2 2.32.10、Release、FreeRTOS 关闭。本机 lv_conf.h 中启用 vector graphics 时也启用了 ThorVG；新版本按实际选项核对。示例不等于产品级 MCU 全外设仿真。
- Serial Studio Pro 4.2.0：官方应用和相同版本桥接。桥接上游路径 `examples/MCP Client/claude_desktop_bridge.py`，使用前核实对应 tag。API 本机参考端口 7777，仅 localhost。许可/试用由用户处理，不分发激活状态。
- Saleae Logic 2.4.48：官方安装；本机曾使用便携展开方式，不能当作新机器的首选安装流程。采集需支持的硬件和驱动，软件 MCP 连接成功不代表硬件采集可用。
- PyQt6 / pyserial / pyqtgraph / pytest / pytest-qt：按具体项目虚拟环境安装，尊重该项目 requirements/pyproject；不因为恢复 skill 就全局 pip 安装 GUI 依赖。

## Node and Bun

- baoyu 两个技能的脚本使用 Bun，可通过 `npx --yes bun` 调用；首次执行可能下载运行时和声明的 npm 依赖。
- 本机测试使用 Bun 1.4.4。固定依赖使用技能自带 lockfile，按脚本目录安装；不要把 node_modules 上传。
- Mermaid 导出图片需要 Chrome/Chromium/Edge；基础 HTML 转换可用 `--no-mermaid` 单独验证，不能把它当作图片渲染已通过。
- 非 Windows 环境优先使用上游版本；Windows 专用改动先比较 PATCHES.md，不盲目覆盖上游已修复实现。

## Minimum validation

1. 清点 skill 名称和来源，确认没有重复安装。
2. UI 检索：`python <SKILL_DIR>/ui-ux-pro-max/scripts/search.py "real-time dashboard" --domain chart -n 1`。
3. 排版：对临时中文文件运行 formatter；检查命令输出和 CJK 间距实际变化，不能只看退出码。
4. HTML：临时 MD 使用 `--theme simple --keep-title --no-mermaid` 转换，检查结果文件。Mermaid 如需使用，再单独测试。
5. MCP：应用启动后初始化和枚举工具；先读状态，再根据当前任务进行设备操作。
6. 编译、PC 单测和真实硬件验证分别记录，不能互相替代。
