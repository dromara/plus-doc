# 2.X项目初始化
- - -
### 项目分支说明

`2.X` 主分支 新2.X版本 稳定发布分支<br>
`dev` 开发分支 代码随时更新 不推荐使用 经测试后会发布到主分支<br>
`future/*` 新功能预览分支

### 项目必备环境
> 推荐使用 `docker` 安装 项目内置 `docker` 编排文件

**注意: 禁止使用 `oraclejdk`(由于spring的bug导致打包运行会报错)**

![输入图片说明](https://foruda.gitee.com/images/1720080025744223375/0213a652_1766278.png "屏幕截图")

* Spring官方推荐使用OpenJDK-17/21 [JDK下载地址](https://bell-sw.com/pages/downloads/) 
* mysql 5.7 8.0 (其他版本未测试 如其他版本没问题 可以告知咱们)
* oracle >= 12c (其他版本未测试 如其他版本没问题 可以告知咱们)
* postgres 13 14 15 (其他版本未测试 如其他版本没问题 可以告知咱们)
* redis 6.X 7.X(禁止使用7.4版本) 由于框架大量使用了redis特性 版本必须 >= 6.X ([win redis 下载地址](https://github.com/zkteco-home/redis-windows))
* minio(RustFS可用于替换minio 比较新需谨慎使用) 本地存储或阿里/腾讯/七牛云等一切支持S3协议的云存储
* (注意 minio最后一个可用版本2025-04-22T22-12-26Z 再往上功能被阉割)
* maven >= 3.8.X
* nodejs 18.18 (其他版本未测试 如其他版本没问题 可以告知咱们)
* npm >= 8.X (7.X确认有问题)
* nacos >= 2.X(建议使用框架内置的 采用nacos官方jar包 做了监控与安全增强)
* sentinel 框架内置(建议使用框架内置的 采用sentinel官方jar包)
* seata 框架内置(建议使用框架内置的 采用seata官方jar包)
* idea 版本避坑指南 看下面:
* 2023(全系列不要用 bug太多说不过来)
* 2024.1/2024.2(maven插件无法刷新依赖)
* 目前推荐使用 2024.3

### 需勾选 maven 对应环境

![输入图片说明](https://foruda.gitee.com/images/1678976284045210056/a2f28d33_1766278.png "屏幕截图")

### 默认 `JDK17` 如有变动 需更改以下配置

![输入图片说明](https://foruda.gitee.com/images/1678941027820943505/c688e01e_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678941120518807034/4d56fcc9_1766278.png "屏幕截图")

### sql导入

将sql导入到与sql文件名对应的数据库(不要放到一个库下)<br>
默认数据库为mysql如需使用其他数据库 看这里 => [多数据库数据源](/ruoyi-cloud-plus/framework/extend/dynamic_datasource.md)<br>

![输入图片说明](https://foruda.gitee.com/images/1717122730708924506/7f3aaecf_1766278.png "屏幕截图")

### 使用内置 `ruoyi-nacos` 服务 从这开始

> 更改 ruoyi-nacos 数据库地址

![输入图片说明](https://foruda.gitee.com/images/1664422006264405180/cac5afc6_1766278.png "屏幕截图")

<font size="4">**其余流程同下方步骤一致**</font>

### 自建 Nacos 从这开始

**注意:使用自建Nacos必须保证版本与框架一致 因为nacos各个版本兼容性不好 建议最好是先用框架自带的**

<font size="4">**Nacos 数据库指向 ry-config 数据库(此处重点: 此数据库为定制数据 未使用此库会无法读取配置)**</font>

> 将项目 `script/config/nacos` 下所有配置 复制到 `nacos` 内(建议手动复制内容 防止编码不一致问题)

**注意: 不懂就不要乱改配置文件内容 框架内所有功能都是配置好的!!!不要画蛇添足**<br>
**注意: 不懂就不要乱改配置文件内容 框架内所有功能都是配置好的!!!不要画蛇添足**<br>
**注意: 不懂就不要乱改配置文件内容 框架内所有功能都是配置好的!!!不要画蛇添足**<br>

![输入图片说明](https://foruda.gitee.com/images/1746693993121928066/26033bb1_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678979856705927770/75cc1e8c_1766278.png "屏幕截图")

> 更改 `主pom文件` 对应环境的 `nacos` 地址

![输入图片说明](https://foruda.gitee.com/images/1678979881888833924/7e6a191f_1766278.png "屏幕截图")

### 更改 `Nacos` 自定义配置

**忠告: 微服务配置相当复杂 请勿在不懂原理的情况下乱改**<br>
**忠告: 微服务配置相当复杂 请勿在不懂原理的情况下乱改**<br>
**忠告: 微服务配置相当复杂 请勿在不懂原理的情况下乱改**<br>

> `application-common.yml` 更改

![输入图片说明](https://foruda.gitee.com/images/1678979889410167794/100db4ab_1766278.png "屏幕截图")

> `datasource.yml` 更改

![输入图片说明](https://foruda.gitee.com/images/1678979894464784408/0d020c07_1766278.png "屏幕截图")

> `seata-server.properties` 更改

![输入图片说明](https://foruda.gitee.com/images/1678979902433843257/12da2839_1766278.png "屏幕截图")

### 使用内置 `ruoyi-seata-server` 服务 从这开始

执行 `ry-seata.sql` 文件 初始化服务端数据库<br>
修改 `nacos` 内的 `seata-server.properties` 的数据库地址<br>
启动 `ruoyi-seata-server` 服务即可

### 服务启动顺序说明

1. 必须启动基础建设: mysql redis nacos<br>
2. 可选启动基础建设: minio(影响文件上传) seata(影响分布式事务 默认开启) sentinel(影响熔断限流) monitor(影响监控) snailjob(影响定时任务)<br>
3. 必须启动应用服务: gateway auth system<br>
4. 可选启动应用服务: resource(影响资源使用 websocket 文件上传 邮件 短信等) workflow(工作流) gen(代码生成) job(影响定时任务) demo(影响demo使用)
