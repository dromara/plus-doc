# 修改应用路径
- - -

## 修改后端路径

修改 `application.yml` 的 `server.servlet.context-path`：

![输入图片说明](https://foruda.gitee.com/images/1724316662536650741/41d534b1_1766278.png "屏幕截图")

开发环境需要同步修改 `vite.config.ts` 的代理路径：

![输入图片说明](https://foruda.gitee.com/images/1724316844091667249/9b0badc5_1766278.png "屏幕截图")

生产环境需修改 `nginx.conf` 后端代理路径：

![输入图片说明](https://foruda.gitee.com/images/1661823876773225117/f1f912a9_1766278.png "屏幕截图")

补充说明：

- 当前前端开发代理默认是 `VITE_APP_BASE_API='/dev-api'`，`vite.config.ts` 会把这个前缀转发到 `http://localhost:8080`。
- 如果后端 `context-path` 从 `/` 改成了例如 `/admin-api`，开发环境至少要同步调整代理目标或重写规则，否则请求会打不到新路径。
- 如果只是 Nginx 层做了反向代理前缀调整，但 Java 应用本身路径没变，则不一定需要改 `context-path`，重点是保持代理映射一致。

## 修改前端路径

`3.4.0` 提供便捷方式：修改 `.env.*` 中 `VITE_APP_CONTEXT_PATH`。

![输入图片说明](https://foruda.gitee.com/images/1661824572484410642/14265f05_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1724317049535973756/0a2cc43b_1766278.png "屏幕截图")

生产环境需要同步修改 `nginx.conf`。  
**注意：真实目录为 `/usr/share/nginx/html/admin/index.html`，多项目部署会增加一层目录，如不需要可自行调整。**

![输入图片说明](https://foruda.gitee.com/images/1678976662194341301/2720b7e9_1766278.png "屏幕截图")

补充说明：

- 当前项目路由基于 `createWebHistory(import.meta.env.VITE_APP_CONTEXT_PATH)` 创建，Vite 打包 `base` 也同样读取这个变量。
- 因此前端访问路径调整时，不仅要改 `.env.*`，还要确认静态资源访问路径、Nginx `location`、刷新路由回退规则一起匹配。
