# 搭建 SnailJob 任务调度中心（2.2.0 新功能）
- - -

## 视频介绍

[Snail job任务调度中心：轻松掌握任务管理、重试机制和任务编排](https://www.bilibili.com/video/BV19i421m7GL/)

## 1. 配置调度中心客户端（主服务）

在主服务配置文件中启用并配置调度中心地址与组信息。

![输入图片说明](https://foruda.gitee.com/images/1716175076777941469/db565dc1_1766278.png "屏幕截图")

字段说明：

- `enabled`：是否启用客户端注册
- `server.server-name`：调度中心服务名（优先从 Nacos 获取）
- `server.address`：调度中心地址（服务名优先，IP 兜底）
- `server.port`：调度中心通信端口
- `token`：组通信校验 token（可在调度中心组配置中更换）
- `group-name`：执行器组名称
- `namespace`：作用域（不同作用域相互隔离，避免填错）

## 2. 启动调度中心

需先执行 `ruoyi-job.sql`，默认账号/密码为 `admin` / `admin`。  
账号信息存储在数据库中，可登录后修改。

![输入图片说明](https://foruda.gitee.com/images/1688634898607827011/8853b387_1766278.png "屏幕截图")

在 `ruoyi-visual -> ruoyi-snailjob-server` 模块启动服务。

![输入图片说明](https://foruda.gitee.com/images/1716175119324078438/ca667a0c_1766278.png "屏幕截图")

注意：此处需修改 **ruoyi-snailjob-server** 的数据库连接配置，支持多种数据库。

![输入图片说明](https://foruda.gitee.com/images/1688013663152608235/6c5d6a9c_1766278.png "屏幕截图")

## 3. 快速入门

[SnailJob 快速入门：基本使用介绍](https://juejin.cn/post/7412955032092442675)
