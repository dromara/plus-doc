# 项目初始化
- - -
### 项目分支说明
`master` 主分支 稳定发布分支<br>
`dev` 开发分支 代码随时更新 不推荐使用 经测试后会发布到主分支<br>
`2.X` 新2.X大版本分支<br>
`future/*` 新功能预览分支

### 项目必备环境
> 推荐使用 `docker` 安装 项目内置 `docker` 编排文件

**注意: 需要使用 `openjdk` 或者 `graalvm` 运行程序 禁止使用 `oraclejdk`(由于spring的bug导致打包运行会报错)**

**graalvm 是oracle旗下的高性能jdk 下载地址: https://www.graalvm.org/downloads/**

* openjdk-17 或 graalvm-22.X-community版本
* mysql 5.7 8.0 (5.6未适配可能会有问题)
* oracle 11g 12c
* postgres 13 14
* redis 5.X 6.X 7.X 由于框架大量使用了redis特性 版本必须 >= 5.X ([win redis 下载地址](https://github.com/zkteco-home/redis-windows))
* minio 本地文件存储 或 阿里云 腾讯云 七牛云等一切支持S3协议的云存储
* maven 3.6.3 3.8.X
* nodejs >= 14
* npm 6.X 8.X (7.X确认有问题)
* nacos >= 2.X(框架1.3.0内置nacos)
* sentinel 框架内置
* seata 框架内置

### 需勾选 maven 对应环境

![输入图片说明](https://foruda.gitee.com/images/1678976284045210056/a2f28d33_1766278.png "屏幕截图")

### 默认 `JDK17` 如有变动 需更改以下配置

![输入图片说明](https://foruda.gitee.com/images/1678941027820943505/c688e01e_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678941120518807034/4d56fcc9_1766278.png "屏幕截图")

### sql导入
将sql导入到与sql文件名对应的数据库(不要放到一个库下)<br>

![输入图片说明](https://foruda.gitee.com/images/1688013241561792410/ad687cb2_1766278.png "屏幕截图")

### 使用内置 `ruoyi-naocs` 服务 从这开始

> 更改 ruoyi-nacos 数据库地址

![输入图片说明](https://foruda.gitee.com/images/1664422006264405180/cac5afc6_1766278.png "屏幕截图")

<font size="4">**其余流程同下方步骤一致**</font>

### 自建 Nacos 从这开始

<font size="4">**Nacos 数据库指向 ry-config 数据库(此处重点: 此数据库为定制数据 未使用此库会无法读取配置)**</font>

> 将项目 `config/nacos` 下所有配置 复制到 `nacos` 内(建议手动复制内容 防止编码不一致问题)

![输入图片说明](https://foruda.gitee.com/images/1678979826345958752/913142c9_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678979856705927770/75cc1e8c_1766278.png "屏幕截图")

> 更改 `主pom文件` 对应环境的 `nacos` 地址

![输入图片说明](https://foruda.gitee.com/images/1678979881888833924/7e6a191f_1766278.png "屏幕截图")

### 更改 `Nacos` 自定义配置

**忠告: 微服务配置相当复杂 请勿在不懂原理的情况下乱改**

> `application.yml` 更改

![输入图片说明](https://foruda.gitee.com/images/1678979889410167794/100db4ab_1766278.png "屏幕截图")

> `datasource.yml` 更改

![输入图片说明](https://foruda.gitee.com/images/1678979894464784408/0d020c07_1766278.png "屏幕截图")

> `seata-server.properties` 更改

![输入图片说明](https://foruda.gitee.com/images/1678979902433843257/12da2839_1766278.png "屏幕截图")

