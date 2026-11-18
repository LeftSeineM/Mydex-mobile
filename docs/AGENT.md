# Mydex-agent · Windows / Linux / macOS

版本：0.1.9 · 2026-11-18

推荐将下面同一段指令发给电脑上的 Agent。它会识别系统与 CPU，下载相应版本。

> 请阅读 https://app.leftseinem.com/agent-guide.html ，根据本机系统和 CPU 架构，从 https://app.leftseinem.com/agent/latest.json 选择并下载匹配的最新版 Mydex-agent，校验后解压并阅读 desktop/headless/skill/SKILL.md。安装到【自选地址，Windows 不推荐 C 盘】，保留已有配置。接入当前工具的 MCP，启用后台自启，不弹命令行、不建桌面快捷方式。优先官方或已有接口，不修改 Coding 工具；先问我用应用版还是网页版，再打开配对二维码，验证实际连接后再报成功。

[按系统下载与完整教程](https://app.leftseinem.com/agent-guide.html) · [固定签名版本索引](https://app.leftseinem.com/agent/latest.json)

- Windows x64：登录启动任务、无窗口宿主。
- Linux x64 / ARM64：systemd 用户服务，后台不依赖 Coding 工具窗口。
- macOS Intel / Apple Silicon：登录用户 LaunchAgent。
- 包内附带 Node 运行时；不安装新的 Coding 工具，不替换原会话。标准 MCP 配置在安装目录 mydex-mcp.json。
- 更新：mydex_check_update 获取匹配本机的签名发布信息，下载校验后使用 mydex_update，并查询实际操作结果。
- 卸载：mydex_uninstall 移除程序和自启，保留配置与兼容桥备份；再删除宿主内的 Mydex MCP 条目。

Linux x64 已在 Ubuntu 24.04 / WSL 验证安装、鉴权 API、二维码生成、标准 MCP、更新保留配置、坏包拒绝、卸载及重装。Windows 隔离升级另做核验。macOS 与 ARM 为预览，尚未做真机端到端验证。各 Coding 工具的原会话能力以实际接口为准。无图形桌面的 Linux 配对需打开返回的本地 HTML 文件；不应发布配对文件。Linux 注销后运行需管理员按需配置 linger；macOS 需登录用户会话。

现有 Mydex-desktop 保留；手机端无需为安装方式更新。此公开包不包含私有 Router/Superagent 灰度功能。
