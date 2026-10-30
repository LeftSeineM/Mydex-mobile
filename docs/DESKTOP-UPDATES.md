# Windows 应用内更新（0.4.8 起）

2026-10-31。

设置页和托盘菜单都有“检查更新”。应用启动后及每 6 小时自动检查，发现新版本会提示，但不自动下载、安装或重启。点击“下载更新”，完成后点击“安装并重启”并确认。

旧版没有此功能，需要先安装一次 0.4.8；之后无需反复到网站下载。

## 更新过程

更新器从自建网站读取 Ed25519 签名清单，使用程序内固定公钥验证；只接受同站点、版本匹配的 HTTPS 安装包，拒绝重定向和降级。下载时校验长度和 SHA-256，安装前再次校验。设置页显示版本、说明和进度。原始签名私钥不包含在程序或仓库中。

独立 PowerShell 更新助手等待界面和桥接器退出，备份程序目录，执行安装包，检查新 EXE 的文件版本，再以托盘模式启动。正常更新不删除 data、网关配置或会话。安装失败会尝试恢复程序备份并显示错误；被外部进程锁定的文件仍可能需要人工处理。日志和备份保留在 D:/Software/MydexDownloads 中。

运行中的连接会短暂中断，用户应等发送或审批完成后再确认安装。安装包不会杀死其他 AI 工具，也不升级模型/API 配置。由外部服务独立管理的网关不由更新器强制重启。

## 发布后续版本

同步更新 desktop/updater.mjs 的 desktopVersion、Mydex.cs 的显示版本及 AssemblyVersion/FileVersion、installer.nsi 和构建输出目录。构建并验证安装包后，使用离线保管的发布私钥签署清单：

```sh
node tools/sign-desktop-release.mjs 0.4.9 dist/Mydex-0.4.9-Setup.exe /private/release-private.pem release-notes.txt desktop-stable.json
```

先上传安装包到 downloads 并核对 SHA，再上传清单至 updates/desktop-stable.json。清单应设置 no-store；应用不接受未签名清单。不得把私钥上传静态网站或提交仓库。

本次验证：版本比较、篡改签名、错误域名/文件名/大小校验测试通过；真实更新源检查和安装包下载通过；本机从旧版安装至 0.4.8.0，原连接配置和证书哈希不变、连接服务恢复。Mac 的应用内更新尚未实现；本说明只适用于 Windows。


## 0.4.9：备用更新源

小主机不可达时，自动从公开 GitHub 仓库 updates/desktop-stable.json 检查同一签名清单，并从对应 desktop-v版本 release 下载同一安装包。只有 GitHub 官方 release-assets / objects 下载域名的 HTTPS 跳转被允许，下载后仍执行相同的签名与大小、哈希校验。国内网络无法访问 GitHub 时仍优先使用原站，两边都不可达则明确报错，不会执行未验证文件。

没有 D 盘的电脑将更新缓存放到安装目录同级的 MydexDownloads 文件夹。真实首轮安装及未来更新都应保留原连接配置。
