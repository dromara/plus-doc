# 修改应用路径
- - -

## 修改后端接口路径

修改前端环境配置中的 `VITE_APP_BASE_API` 代理路径：

![输入图片说明](https://foruda.gitee.com/images/1661824572484410642/14265f05_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1724317552931269967/f7515655_1766278.png "屏幕截图")

生产环境需同步修改 `nginx.conf` 后端代理路径。

![输入图片说明](https://foruda.gitee.com/images/1678980501204821424/d3340308_1766278.png "屏幕截图")

补充说明：

- `VITE_APP_BASE_API` 是前端本地开发和部署时统一使用的“代理前缀”，当前默认值是 `/dev-api`。
- 它和网关里的业务路由前缀不是同一个概念。比如前端真实请求通常是 `/dev-api/system/user/list`，经过代理后才转发成网关里的 `/system/user/list`。
- 如果你改的是代理前缀，只需要同步前端环境变量、Vite 代理配置、Nginx 反向代理配置。
- 如果你改的是业务模块路由前缀，例如把网关里的 `/system/**` 改成 `/admin-system/**`，那前端接口地址、网关路由配置也都要同步修改。
- 网关路由请同步检查 `script/config/nacos/ruoyi-gateway.yml` 或 `ruoyi-gateway-mvc.yml`。

## 修改前端页面访问路径

修改 `.env.*` 中 `VITE_APP_CONTEXT_PATH`：

![输入图片说明](https://foruda.gitee.com/images/1661824572484410642/14265f05_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1724317049535973756/0a2cc43b_1766278.png "屏幕截图")

生产环境需同步修改 `nginx.conf`。  
**注意：真实目录为 `/usr/share/nginx/html/admin/index.html`，多项目部署会增加一层目录，如不需要可自行调整。**

![输入图片说明](https://foruda.gitee.com/images/1678976662194341301/2720b7e9_1766278.png "屏幕截图")
