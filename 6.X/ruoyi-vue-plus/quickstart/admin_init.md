# 搭建 Admin 监控
- - -

## 1. 配置监控客户端（主服务）

在主服务配置文件中启用并配置监控中心地址与账号。

![输入图片说明](https://foruda.gitee.com/images/1678941504260707700/68ab99e5_1766278.png "屏幕截图")

字段说明：

- `enabled`：是否启用客户端注册
- `url`：监控中心地址
- `username` / `password`：监控中心登录账号

示例：

- `url`：`http://localhost:9090`（以实际部署为准）

## 2. 启动监控中心

在 `扩展项目 -> 监控模块` 启动对应服务。

![输入图片说明](https://foruda.gitee.com/images/1678976327174539378/df97e36e_1766278.png "屏幕截图")

监控模块的 `yml` 文件中可设置登录账号、密码与访问路径。

![输入图片说明](https://foruda.gitee.com/images/1678941572583282843/28117457_1766278.png "屏幕截图")

## 3. 前端访问路径配置

### 3.1 开发环境

`dev` 环境使用 `.env.development` 中的监控中心地址。

![输入图片说明](https://foruda.gitee.com/images/1678941607472644388/460e8eea_1766278.png "屏幕截图")

### 3.2 生产环境

`prod` 环境使用 `.env.production` 的本机路由，通常通过 Nginx 反向代理转发。

![输入图片说明](https://foruda.gitee.com/images/1678941644784144830/6293ab1c_1766278.png "屏幕截图")

因此生产环境只需调整 `nginx` 代理路径即可。

![输入图片说明](https://foruda.gitee.com/images/1678981483900657668/31fd1aad_1766278.png "屏幕截图")
