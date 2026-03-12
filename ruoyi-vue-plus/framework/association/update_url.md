# 修改应用路径
- - -

## 修改后端路径

修改 `application.yml` 的 `server.servlet.context-path`：

![输入图片说明](https://foruda.gitee.com/images/1724316662536650741/41d534b1_1766278.png "屏幕截图")

开发环境需要同步修改 `vite.config.ts` 的代理路径：

![输入图片说明](https://foruda.gitee.com/images/1724316844091667249/9b0badc5_1766278.png "屏幕截图")

生产环境需修改 `nginx.conf` 后端代理路径：

![输入图片说明](https://foruda.gitee.com/images/1661823876773225117/f1f912a9_1766278.png "屏幕截图")

## 修改前端路径

`3.4.0` 提供便捷方式：修改 `.env.*` 中 `VITE_APP_CONTEXT_PATH`。

![输入图片说明](https://foruda.gitee.com/images/1661824572484410642/14265f05_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1724317049535973756/0a2cc43b_1766278.png "屏幕截图")

生产环境需要同步修改 `nginx.conf`。  
**注意：真实目录为 `/usr/share/nginx/html/admin/index.html`，多项目部署会增加一层目录，如不需要可自行调整。**

![输入图片说明](https://foruda.gitee.com/images/1678976662194341301/2720b7e9_1766278.png "屏幕截图")
