# 修改应用路径
- - -

## 修改后端接口路径

修改前端环境配置中的 `VITE_APP_BASE_API` 代理路径：

![输入图片说明](https://foruda.gitee.com/images/1661824572484410642/14265f05_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1724317552931269967/f7515655_1766278.png "屏幕截图")

生产环境需同步修改 `nginx.conf` 后端代理路径。

![输入图片说明](https://foruda.gitee.com/images/1678980501204821424/d3340308_1766278.png "屏幕截图")

## 修改前端页面访问路径

修改 `.env.*` 中 `VITE_APP_CONTEXT_PATH`：

![输入图片说明](https://foruda.gitee.com/images/1661824572484410642/14265f05_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1724317049535973756/0a2cc43b_1766278.png "屏幕截图")

生产环境需同步修改 `nginx.conf`。  
**注意：真实目录为 `/usr/share/nginx/html/admin/index.html`，多项目部署会增加一层目录，如不需要可自行调整。**

![输入图片说明](https://foruda.gitee.com/images/1678976662194341301/2720b7e9_1766278.png "屏幕截图")
