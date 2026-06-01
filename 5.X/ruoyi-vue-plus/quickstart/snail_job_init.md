# 搭建 SnailJob 任务调度中心（5.2.0 新功能）
- - -

## 视频介绍

[Snail job任务调度中心：轻松掌握任务管理、重试机制和任务编排](https://www.bilibili.com/video/BV19i421m7GL/)

## 1. 配置调度中心客户端（主服务）

在主服务配置文件中启用并配置调度中心地址与组信息。

![输入图片说明](https://foruda.gitee.com/images/1687656939847353725/951c1af7_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1716174758437043952/de28db71_1766278.png "屏幕截图")

字段说明：

- `enabled`：是否启用客户端注册
- `server.address`：调度中心地址
- `server.port`：调度中心通信端口
- `token`：组通信校验 token（可在调度中心组配置中更换）
- `group-name`：执行器组名称
- `namespace`：作用域（不同作用域相互隔离，避免填错）

## 2. 启动调度中心

需先执行 `ry_job.sql`，默认账号 `admin`、默认密码 `admin`。  
账号信息存储在数据库中，可登录后修改。

![输入图片说明](https://foruda.gitee.com/images/1726801238503062021/a030616f_1766278.png "屏幕截图")

在 `ruoyi-extend -> ruoyi-snailjob-server` 模块启动服务。

![输入图片说明](https://foruda.gitee.com/images/1716174842485474283/78cec86d_1766278.png "屏幕截图")

注意：此处需修改 **ruoyi-snailjob-server** 的数据库连接配置，支持多种数据库。

![输入图片说明](https://foruda.gitee.com/images/1714356048711590477/13289085_1766278.png "屏幕截图")

## 3. 快速入门

[SnailJob 快速入门：基本使用介绍](https://juejin.cn/post/7412955032092442675)

## 4. 前端访问路径配置

### 4.1 开发环境

`dev` 环境默认使用 `.env.development` 中的地址。

![输入图片说明](https://foruda.gitee.com/images/1716174933143893408/58d47bbc_1766278.png "屏幕截图")

### 4.2 生产环境

`prod` 环境使用 `.env.production` 的本机路由，通常通过 Nginx 反向代理转发。

![输入图片说明](https://foruda.gitee.com/images/1716174973454805690/0d6f20fb_1766278.png "屏幕截图")

因此生产环境只需调整 `nginx` 反向代理路径即可。

![输入图片说明](https://foruda.gitee.com/images/1716174998979181179/2f9e4e4a_1766278.png "屏幕截图")
