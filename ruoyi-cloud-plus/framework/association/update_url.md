# 修改应用路径
- - -
# 修改访问后端接口路径

更改 前端环境配置文件 `VUE_APP_BASE_API` 代理路径

![输入图片说明](https://images.gitee.com/uploads/images/2022/0623/174450_522eabdf_1766278.png "屏幕截图.png")<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0623/174338_2a0b059d_1766278.png "屏幕截图.png")

`prod` 生产环境需修改 `nginx.conf` 后端代理路径(上述配置文件也要改)

![输入图片说明](https://images.gitee.com/uploads/images/2022/0623/180742_18831b18_1766278.png "屏幕截图.png")

# 修改前端页面访问路径
修改对应环境的 `.env.环境` 文件内的 `VUE_APP_CONTEXT_PATH` 应用访问路径即可

![输入图片说明](https://foruda.gitee.com/images/1661824572484410642/14265f05_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1661824554927577058/af022983_1766278.png "屏幕截图")

生产环境 `nginx.conf` 与之对应修改即可<br>
**注意: 文件真实目录为 `/usr/share/nginx/html/admin/index.html` 此功能一般为多项目部署需要 故会增加一层目录 如不需要可以自行修改**<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0409/131009_d8a9b724_1766278.png "屏幕截图.png")