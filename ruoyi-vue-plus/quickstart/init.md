# 5.X项目初始化
- - -
### 项目分支说明

`5.X` 主分支 5.X版本 稳定发布分支<br>
`dev` 开发分支 代码随时更新 不推荐使用 经测试后会发布到主分支<br>
`future/*` 新功能预览分支<br>

### 项目必备环境
> 推荐使用 `docker` 安装 项目内置 `docker` 编排文件

**注意: 需要使用 `openjdk` 或者 `graalvm` 运行程序 禁止使用 `oraclejdk`(由于spring的bug导致打包运行会报错)**

**graalvm 是oracle旗下的高性能jdk 下载地址: https://github.com/graalvm/graalvm-ce-builds/releases**

* openjdk-17/21 或 graalvm-community-jdk-17/21 版本
* mysql 5.7 8.0 (5.6未适配可能会有问题)
* oracle 11g 12c
* postgres 13 14
* sqlserver 2017 2019
* redis 5.X 6.X 7.X 由于框架大量使用了redis特性 版本必须 >= 5.X ([win redis 下载地址](https://github.com/zkteco-home/redis-windows))
* minio 本地文件存储 或 阿里云 腾讯云 七牛云等一切支持S3协议的云存储
* maven >= 3.8.X
* nodejs 18(18以上未测试 不建议使用)
* npm 8.X (7.X确认有问题)
* idea 2022 2024 (一定不要使用2023后果自负 bug太多影响项目开发)

### 搭建视频

[RuoYi-Vue-Plus 5.0 搭建与运行](https://www.bilibili.com/video/BV1Fg4y137JK/)

### 勾选maven对应环境
![输入图片说明](https://foruda.gitee.com/images/1678976284045210056/a2f28d33_1766278.png "屏幕截图")

### 默认 `JDK17` 如有变动 需更改以下配置

![输入图片说明](https://foruda.gitee.com/images/1678941027820943505/c688e01e_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678941120518807034/4d56fcc9_1766278.png "屏幕截图")

### sql导入

请按照以下顺序依次导入 默认为 `mysql` 其他数据库需导入对应的sql文件

![输入图片说明](https://foruda.gitee.com/images/1688634217677295748/f9919efd_1766278.png "屏幕截图")

工作流sql导入

![输入图片说明](https://foruda.gitee.com/images/1714211018405279764/013abc6d_5363069.png "屏幕截图")

版本更新

![输入图片说明](https://foruda.gitee.com/images/1688634290787855369/c09c268f_1766278.png "屏幕截图")



**多数据库支持 5.X 调度中心采用 PowerJob 底层为 JPA 支持所有数据库**

### 服务启动顺序说明

1. 必须启动基础建设: mysql redis admin<br>
2. 可选启动基础建设: minio(影响文件上传) monitor(影响监控) powerjob(影响定时任务)<br>

![输入图片说明](https://foruda.gitee.com/images/1678976302776168895/7333341c_1766278.png "屏幕截图")
* `MonitorAdminApplication` 为 Admin监控服务(非必要 可参考对应文档关闭 [搭建Admin监控](/ruoyi-vue-plus/quickstart/admin_init.md))
* `EasyRetryServerApplication` 为 任务调度中心服务(非必要 可参考对应文档关闭 [搭建调度中心](/ruoyi-vue-plus/quickstart/snail_job_init.md))
* `DromaraApplication` 为 主应用服务
> 需优先启动 `MonitorAdminApplication` 与 `EasyRetryServerApplication` 具体配置方式参考对应文档<br>
> 最后启动 主服务 `DromaraApplication`<br>
> 工作流相关初始化使用 [工作流初始化](/ruoyi-vue-plus/quickstart/worker_init.md)

### 主服务配置方式

在勾选对应环境的配置文件内 填写 mysql 与 redis 配置信息

![输入图片说明](https://foruda.gitee.com/images/1678941357316005626/70559736_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1678941405169571070/0d06a955_1766278.png "屏幕截图")

其他数据库配置 按照系统自带的配置更改即可

![输入图片说明](https://foruda.gitee.com/images/1678941444707120259/b274592a_1766278.png "屏幕截图")