# Mydex 网页中继 v2

2026-10-30。Android 保持原 APK；iPhone / 纯血鸿蒙用网页；电脑继续本机 Mydex。

入口：https://app.leftseinem.dpdns.org/connect/
教程：https://app.leftseinem.dpdns.org/apple-guide.html

## 使用

Windows 安装 0.4.12，配置本机并启动连接，选择“配对手机 → 网页版 → 生成配对二维码”。在网页用自己的邮箱接收验证码并注册、登录，点击“扫描电脑配对码”或从相册读取二维码，核对六位确认码并确认。电脑在线后打开会话。每台电脑分别配对，无需公网 IP 和端口映射。账号页面可解除绑定。Mac 源码加入同样入口，构建和真机验证单独记录。

## 架构

网页 → 自建中继 → 电脑主动建立的 WSS → 本机 HTTPS 网关 → 现有工具。

密码通过随机盐和 scrypt 派生后存储；登录使用 Secure / HttpOnly / SameSite=Strict Cookie，7 天有效，中继重启需要重新登录。配对二维码 5 分钟有效、一次性；电脑持有独立轮询秘密。每次请求校验账号与电脑归属，WebSocket 使用绑定会话和电脑、30 秒有效的一次性票据。注销及解除绑定关闭已有连接。

电脑连接令牌在中继仅存哈希，原始令牌存于电脑本地数据目录。中继不接收本机网关令牌或模型密钥，只允许任务相关 API，不接受任意目标 URL、文件路径或执行命令。中继能处理转发内容，不是端到端加密；不保存对话历史，应用日志不输出正文或令牌。网站现有隧道供应商参与网络传输，不能宣称没有第三方网络设施。

没有邮件找回服务，请保存密码。账号删除接口需再次验证密码。登录与配对有速率限制，每账号最多 50 台电脑。

## 构建

当前发布固定 Flutter 3.27.4，HTML renderer 使用系统字体，避免字体 CDN 并降低首次加载负担。该 renderer 已弃用，未来升级 Flutter 时必须迁移和重新验证。

```sh
flutter pub get
flutter build web --release --base-href /web/ --web-renderer html --pwa-strategy=none --no-web-resources-cdn
python tools/prepare-web.py
```

将 build/web 部署到 /web/，启用 nginx gzip_static。HTML/bootstrap 使用 no-cache；当前不启用离线 service worker。Manifest 从 /connect/ 启动。

## 中继部署

安装 gateway 的 ws 依赖，运行 `node gateway/relay.mjs /private/relay-config.json`。

```json
{"origin":"https://your.example","host":"127.0.0.1","port":18083,"dataFile":"/private/accounts.json"}
```

反向代理将 /connect/*、/relay/*、/c/* 转发到中继，保留 Cookie、Origin、Authorization 和 WebSocket Upgrade，其余路径继续静态网站。不记录查询串（含短时票据）。电脑可用 MYDEX_RELAY_ORIGIN 环境变量指定自己的 HTTPS 中继。账号数据库不能放入网站目录。

## 验证边界

relay.test.mjs、gateway.test.mjs、web-access.test.mjs 验证账号隔离、配对重放、HTTP/WS 转发、请求去重、撤销和来源限制。公网发送测试使用模拟电脑，不调用模型、不向用户原会话写测试消息。手机尺寸及折叠屏截图来自桌面浏览器，不等同于 iPhone / 鸿蒙真机验证。


## 网页版 2026.10.31.1

历史版本曾关闭公开注册；2026.10.31.2 已改为邮箱验证码注册（2026-11-01 上线），旧测试账号停止登录，原数据保留，新账号需重新配对自己的电脑。登录页和原有设置页均可调节字体 60%–200%；字号只保存在当前浏览器，不按账号跨手机同步。清除浏览器站点数据会重置字号。

电脑选择框旁的垃圾桶可解除当前账号绑定，不删除电脑文件或原对话。新版 Windows 0.4.12 重复扫码会复用同一电脑绑定；不同电脑同名不会误合并。老版本造成的无身份记录需手动删除。

网页统一使用本站 Noto Sans SC 字体，减少中英文混排错位，无外部字体请求。浏览器模拟手机测试通过，华为真机效果仍需实际确认。


## 网页版：注册、验证码登录与扫码配对

更新：2026-11-01，网页版本 2026.11.01.4。

1. [打开网页版](https://app.leftseinem.dpdns.org/connect/)，用自己的邮箱验证注册。已有账号可选择邮箱验证码登录或密码登录。
2. 电脑打开 Mydex → 配对手机 → 网页版，生成二维码。
3. 手机网页点击“扫描电脑配对码”，也可从相册读取；核对确认码后绑定。
4. 电脑在线后打开会话。相同账号换设备保留绑定，历史对话从自己的在线电脑加载，不同账号隔离。

验证码十分钟内有效且仅用一次。浏览器完整链路及账号隔离测试通过；手机物理摄像头仍待真机复测。详见[网页教程](https://app.leftseinem.dpdns.org/apple-guide.html)。
