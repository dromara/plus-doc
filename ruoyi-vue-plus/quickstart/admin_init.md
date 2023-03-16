# 搭建Admin监控
- - -
### 配置监控客户端

> 修改主服务配置文件

![输入图片说明](https://images.gitee.com/uploads/images/2021/1012/125136_28781454_1766278.png "屏幕截图.png")

* `enabled` 可启用或关闭客户端注册
* `url` 为监控中心地址
* `username 与 password` 为监控中心的账号密码

### 启用监控中心
在 `扩展项目 -> 监控模块` 启动

![输入图片说明](https://images.gitee.com/uploads/images/2021/1012/124911_85311d84_1766278.png "屏幕截图.png")

在监控模块对应的 `yml` 配置文件 可设置登录的账号密码与访问路径

![输入图片说明](https://images.gitee.com/uploads/images/2021/1012/125625_47e77f89_1766278.png "屏幕截图.png")

### 前端修改admin监控访问路径
`dev`环境 默认使用 `.env.development` 配置文件内地址

![输入图片说明](https://images.gitee.com/uploads/images/2021/1012/130306_65499b87_1766278.png "屏幕截图.png")

`prod`环境 使用 `.env.production` 本机路由

![输入图片说明](https://images.gitee.com/uploads/images/2021/1012/130418_446f169b_1766278.png "屏幕截图.png")
故而 `prod` 环境只需更改 `nginx` 反向代理路径即可

![输入图片说明](https://images.gitee.com/uploads/images/2021/1012/130511_54e91692_1766278.png "屏幕截图.png")
