### 项目分支说明
`4.X` 主分支 4.X版本 稳定发布分支
`fast` 单体分支 功能与主分支相同 结构为单模块
`dev` 开发分支 代码随时更新 不推荐使用 经测试后会发布到主分支
`future/*` 新功能预览分支

### 项目必备环境
> 推荐使用 `docker` 安装 项目内置 `docker` 编排文件
* oracle jdk 8 11 (暂时不支持 17 不支持大于 jdk8_202 因为202是最后一个免费版本)
* mysql 5.7 8.0 (5.6未适配可能会有问题)
* oracle 11g 12c
* postgres 13 14
* sqlserver 2017 2019
* redis 5.X 6.X 由于框架大量使用了redis特性 版本必须 >= 5.X ([win redis 下载地址](https://github.com/tporadowski/redis))
* minio 本地文件存储 或 阿里云 腾讯云 七牛云等一切支持S3协议的云存储
* maven 3.6.3 3.8.X
* nodejs >= 12
* npm 6.X 8.X (7.X确认有问题)

### 3.2.0及以上 只需勾选对应环境即可
![输入图片说明](https://images.gitee.com/uploads/images/2021/0914/121055_05a47002_1766278.png "屏幕截图.png")

### 默认 `JDK1.8` 如有变动 需更改以下配置

![输入图片说明](https://images.gitee.com/uploads/images/2021/1117/195230_de79cafc_1766278.png "屏幕截图.png")
![输入图片说明](https://images.gitee.com/uploads/images/2021/1117/195254_d411683d_1766278.png "屏幕截图.png")
![输入图片说明](https://images.gitee.com/uploads/images/2021/1117/195330_3372c392_1766278.png "屏幕截图.png")

### sql导入

请按照以下顺序依次导入

![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/105532_fc1c3bd8_1766278.png "屏幕截图.png")

默认为 `mysql` 其他数据库需导入对应的sql文件

![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/105439_dce3b512_1766278.png "屏幕截图.png")

**多数据库仅支持主应用 扩展应用需自行适配(例如: xxl-job仅支持mysql)**

### 应用启动
应用列表

![输入图片说明](https://images.gitee.com/uploads/images/2021/1027/103354_d2294981_1766278.png "屏幕截图.png")
* `MonitorAdminApplication` 为 Admin监控服务(非必要 可参考对应文档关闭)
* `XxlJobAdminApplication` 为 任务调度中心服务(非必要 可参考对应文档关闭)
* `RuoYiApplication` 为 主应用服务
> 需优先启动 `MonitorAdminApplication` 与 `XxlJobAdminApplication` 具体配置方式参考对应文档
> 最后启动 主服务 `RuoYiApplication`

### 主服务配置方式

在勾选对应环境的配置文件内 填写 mysql 与 redis 配置信息

![输入图片说明](https://images.gitee.com/uploads/images/2021/0623/211135_daea1338_1766278.png "屏幕截图.png")

![输入图片说明](https://images.gitee.com/uploads/images/2021/0623/211156_86fdefac_1766278.png "屏幕截图.png")

其他数据库配置 按照系统自带的配置更改即可

![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/110443_3ca4205a_1766278.png "屏幕截图.png")


