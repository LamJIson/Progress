## Cloudflare-pages代理脚本:

### PAGES部署实现VLESS+WS+TLS。

### 基础部署视频教程：https://www.youtube.com/watch?v=LeT4jQUh8ok

------------------------------------------------------------------------
## CF vless代码（_worker.js文件）可修改内容及说明:

### 1、UUID须自定义。

### 2、ProxyIP来源于网上各位大佬的分享，可通过path自定义。

### 3、伪装网页设置为librespeed.speedtestcustom.com，可自定义。

### 4、订阅地址：https://[YOUR-PAGES-URL]/[YOUR-UUID]，即可获取订阅内容。

### 5、支持Base64、clash-meta、sing-box订阅格式, 订阅由vless.fxxk.dedyn.io提供维护支持。


------------------------------------------------------------------------
</details>

## Pages 部署方法
1. 部署 Cloudflare Pages：
   - 在 Github 上先 Fork 本项目，并点上 Star !!!
   - 在 Cloudflare Pages 控制台中选择 `连接到 Git`后，选中 `edgetunnel`项目后点击 `开始设置`。
   - 在 `设置构建和部署`页面下方，选择 `环境变量（高级）`后并 `添加变量`
     变量名称填写**UUID**，值则为你的UUID，后点击 `保存并部署`即可。

2. 给 Pages绑定 CNAME自定义域：
   - 在 Pages控制台的 `自定义域`选项卡，下方点击 `设置自定义域`。
   - 填入你的自定义次级域名，注意不要使用你的根域名。例如： 您分配到的域名是 `fuck.cloudns.biz`，则添加自定义域填入 `lizi.fuck.cloudns.biz`即可
   - 按照 Cloudflare 的要求将返回你的域名DNS服务商，添加 该自定义域 `shili`的 CNAME记录 `edgetunnel.pages.dev` 后，点击 `激活域`即可。

3. 给 Pages设定 环境变量：
   - 在 Pages控制台的 `设置`选项卡，下方点击 `环境变量`。
   - 填入你的环境变量，注意使用大写，例如：UUID、SOCKS5（若有推荐优先）、RPROXYIP（需订阅器支持）、SUBAPI、SUBCONFIG

4. 使用自己的`优选域名`/`优选IP`的订阅内容(可选)：
   - 当您使用 `let sub = 'sub.cmliussss.workers.dev';` 等非空参数时，您的worker节点配置将通过指定的订阅生成器创建完整的节点订阅信息。这种方式确实便捷，但同时意味着您的节点配置信息将被发送给订阅服务的提供者。
   - 如果您对此存有顾虑，可以通过将 `let sub = '';` 设置为空值，以保持您的edgetunnel节点配置的私密性。但这种方式需要您自行手动选择优选IP或域名，却更能保障你的信息安全；
   - 如果你想使用自己的优选域名或者是自己的优选IP，可以参考 [WorkerVless2sub GitHub 仓库](https://github.com/cmliu/WorkerVless2sub) 中的部署说明自行搭建。
   - 在 Pages控制台的 `设置`选项卡，选择 `环境变量`> `制作`> `编辑变量`> `添加变量`；
   - 变量名设置为`SUB`，对应的值为你部署的订阅生成器地址。例如 `sub.cmliussss.workers.dev`，后点击 **保存**。
   - 之后在 Pages控制台的 `部署`选项卡，选择 `所有部署`> `最新部署最右的 ...`> `重试部署`，即可。
   - 注意，如果您使用了自己的订阅地址，要求订阅生成器的 `SUB`域名 和 `[YOUR-PAGES-URL]`的域名 不同属一个顶级域名，否则会出现异常。您可以在 `SUB` 变量赋值为 Pages.dev 分配到的域名。

6. 解决转换订阅的隐私问题(可选)：
   - 搭建反代订阅转换工具，通过随机化服务器地址和节点账号密码，解决用户转换订阅的隐私问题。
   - 可以参考[不良林psub项目](https://github.com/bulianglin/psub)自行搭建，视频原理以及教程 https://youtu.be/X7CC5jrgazo
   - 在 Pages控制台的 `设置`选项卡，选择 `环境变量`> `制作`> `编辑变量`> `添加变量`；
   - 变量名设置为`SUBAPI`，对应的值为你部署的订阅生成器地址。例如 `psub.cmliucdn.workers.dev`，后点击 **保存**。注意不要带https等协议信息和符号。
   - 之后在 Pages控制台的 `部署`选项卡，选择 `所有部署`> `最新部署最右的 ...`> `重试部署`，即可。
   - 注意，如果您使用了反代订阅转换工具，要求订阅转换工具的 `SUBAPI`域名 和 `[YOUR-PAGES-URL]`的域名 不同属一个顶级域名，否则会出现异常。您可以在 `SUBAPI` 变量赋值为 workers.dev 分配到的域名，注意不要带https等协议信息和符号。

</details>

### 变量说明
| 变量名 | 参考示例 | 备注 | 
|--------|---------|-----|
| UUID | xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx | Powershell -NoExit -Command "[guid]::NewGuid()"|
| SOCKS5  | user:password@127.0.0.1:1080 | 优先作为访问CloudFlareCDN站点的SOCKS5代理 |
| RPROXYIP | true | 设为 true 即可强制获取订阅器分配的ProxyIP(需订阅器支持) |
| SUBAPI | api.v1.mk | clash、singbox等 订阅转换后端 |
| SUBCONFIG | [https://raw.github.../ACL4SSR_Online_Full_MultiMode.ini](https://raw.githubusercontent.com/cmliu/edgetunnel/main/Clash/config/ACL4SSR_Online_Full_MultiMode.ini) | clash、singbox等 订阅转换配置文件 |

------------------------------------------------------------------------
## 感谢：

### CF-vless代码作者[zizifn](https://github.com/zizifn/edgetunnel)。
### CF-vless代码作者[3Kmfi6HP](https://github.com/3Kmfi6HP/EDtunnel)。
### CF-vless订阅生成作者[cmliu](https://github.com/cmliu/WorkerVless2sub)。
### CF-vless订阅转换作者[bulianglin](https://github.com/bulianglin/psub)。
### CF优选IP程序作者[badafans](https://github.com/badafans/Cloudflare-IP-SpeedTest)、[XIU2](https://github.com/XIU2/CloudflareSpeedTest)。

------------------------------------------------------------------------
## 声明：

### 所有代码来源于Github社区与ChatGPT的整合；如您需要开源代码，请提Issues留下您的联系邮箱。

------------------------------------------------------------------------
