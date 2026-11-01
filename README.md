<div align="center">

# Mydex

**把电脑上的编程对话，带到手机上。**

[下载安装](https://app.leftseinem.dpdns.org/) · [打开网页版](https://app.leftseinem.dpdns.org/connect/) · [完整教程](docs/GETTING-STARTED.md) · [问题反馈](https://github.com/LeftSeineM/Mydex-mobile/issues)

</div>

Mydex 连接你自己的电脑，让你在手机上查看项目和已有对话，跟进任务并与已适配的工具交互。模型账号、API 配置和任务执行留在电脑端。

## 快速开始

1. **在电脑上安装 Mydex。** 打开 [下载页面](https://app.leftseinem.dpdns.org/)，选择 Windows 或 Mac 版本。建议把下面这段话交给电脑上的 AI 助手，协助安装和检查：

   > 请从 https://app.leftseinem.dpdns.org/ 下载适合这台电脑的 Mydex，安装到我选择的位置并保留已有配置。检查 Coding 工具和原会话的接入，问我使用手机网页版还是 Android 应用版，再启动连接并打开对应配对二维码。需要登录、授权或扫码时告诉我，不要泄露密钥；未实际连通不要说成功。

2. **选择手机使用方式。** Android 可安装 APK；iPhone、纯血鸿蒙及其他支持现代浏览器的设备可打开 [网页版](https://app.leftseinem.dpdns.org/connect/)并按提示登录。
3. **扫码配对。** 电脑打开 Mydex 的「配对手机」，选择与手机一致的方式，生成二维码；手机添加电脑并扫码。每台电脑分别配对。
4. **打开会话。** 保持电脑和需要使用的 Coding 工具运行，在手机选择电脑、工具、项目和会话。支持的操作以工具和实际连接状态为准。

[图文安装与配对教程 →](docs/GETTING-STARTED.md) · [网页版教程 →](docs/WEB.md) · [Mac 安装说明 →](docs/MACOS.md)

如果安装或连接遇到问题，也可以把下面这句话交给电脑上的 AI 助手：

> 请检查并修复本机 Mydex 安装和连接，应用位于【填写安装位置】。保留已有配置，确认服务就绪后打开手机配对二维码；需要我扫码或授权时告诉我，不要泄露密钥。

使用 VPN 时建议选择规则／分流模式；连接失败时可关闭全局／TUN 模式后重试。手机删除电脑：**设置 → 管理已添加电脑**。

## 界面一览

<table><tr><th>手机项目与对话</th><th>对话与运行步骤</th></tr><tr><td><img src="docs/images/projects.png" width="300" alt="手机项目列表" /></td><td><img src="docs/images/conversation.png" width="300" alt="手机对话页面" /></td></tr></table>

<table><tr><th>折叠屏双栏</th><th>电脑连接与工具</th></tr><tr><td><img src="docs/images/foldable.png" width="500" alt="折叠屏双栏页面" /></td><td><img src="docs/images/desktop-tools.png" width="500" alt="电脑工具页面" /></td></tr></table>

截图使用演示数据；详细功能和各工具的实际适配条件见下方文档。

## 功能与使用说明

- **多电脑**：每台电脑单独配对，手机集中选择；可删除不再使用的设备。
- **多工具与原会话**：电脑端负责检测和接入 Coding 工具。是否能查看、继续发言或使用审批等功能，取决于工具、版本及适配状态。
- **任务过程**：查看消息、运行步骤和截图；长内容与批量脚本支持收起。
- **手机与折叠屏**：字号可调，宽屏展开时可并排查看导航与对话。
- **连接方式**：应用版优先尝试直连，必要时使用加密备用通道；网页版依赖中继和在线电脑。不同网络条件下的连通性可能不同。

[完整功能图解](docs/FEATURES.md) · [全部页面截图](docs/SCREENSHOTS.md) · [连接与网络说明](docs/ANDROID-MESH.md) · [权限与审批](docs/PERMISSIONS.md)

## 反馈与项目说明

[提交问题](https://github.com/LeftSeineM/Mydex-mobile/issues) · [邮件联系开发者：348897402@qq.com](mailto:348897402@qq.com)

反馈时请说明使用的工具、操作步骤和错误提示；截图中请遮盖访问令牌、API Key 和配对信息。

本仓库公开提供下载、教程和截图；应用源码独立维护于私有仓库。Mydex 不是相关 AI 工具厂商的官方客户端。
