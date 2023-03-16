# 项目初始化
- - -
### 项目分支说明
`master` 主分支 稳定发布分支<br>
`dev` 开发分支 代码随时更新 不推荐使用 经测试后会发布到主分支<br>
`future/*` 新功能预览分支

### 项目必备环境
> 推荐使用 `docker` 安装 项目内置 `docker` 编排文件

* oracle jdk 8 11 (暂时不支持 17 不支持大于 jdk8_202 因为202是最后一个免费版本)
* mysql 5.7 8.0 (5.6未适配可能会有问题)
* oracle 11g 12c
* postgres 13 14
* redis 5.X 6.X 由于框架大量使用了redis特性 版本必须 >= 5.X ([win redis 下载地址](https://github.com/tporadowski/redis))
* minio 本地文件存储 或 阿里云 腾讯云 七牛云等一切支持S3协议的云存储
* maven 3.6.3 3.8.X
* nodejs >= 12
* npm 6.X 8.X (7.X确认有问题)
* nacos >= 2.X(框架1.3.0内置nacos)
* sentinel 框架内置
* seata 框架内置

### 需勾选 maven 对应环境
![输入图片说明](https://images.gitee.com/uploads/images/2022/0224/143021_2c9f9ddd_1766278.png "屏幕截图.png")

### 默认 `JDK1.8` 如有变动 需更改以下配置
![输入图片说明](https://images.gitee.com/uploads/images/2022/0224/143140_436fbc05_1766278.png "屏幕截图.png")
![输入图片说明](https://images.gitee.com/uploads/images/2022/0224/143237_d9af6aa4_1766278.png "屏幕截图.png")
![输入图片说明](https://images.gitee.com/uploads/images/2022/0224/143322_3e1ab652_1766278.png "屏幕截图.png")

### sql导入
将sql导入到与sql文件名对应的数据库(不要放到一个库下)<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0727/103241_53db9b6c_1766278.png "屏幕截图.png")

### 框架 >= 1.3.0 可直接使用内置 `ruoyi-naocs` 服务

更改 ruoyi-nacos 数据库地址
![输入图片说明](https://foruda.gitee.com/images/1664422006264405180/cac5afc6_1766278.png "屏幕截图")

**其余流程同下方步骤一致**

### 自建 Nacos 或 框架 < 1.3.0 配置 Nacos

**Nacos 数据库指向 ry-config 数据库(此处重点: 此数据库为定制数据 未使用此库会无法读取配置)**

> 将项目 `config` 下所有配置 复制到 `nacos` 内(建议手动复制内容 防止编码不一致问题)

![输入图片说明](https://images.gitee.com/uploads/images/2022/0224/143745_68389680_1766278.png "屏幕截图.png")
![输入图片说明](https://images.gitee.com/uploads/images/2022/0301/151107_9c5072ef_1766278.png "屏幕截图.png")

> 更改 `主pom文件` 对应环境的 `nacos` 地址

![输入图片说明](https://images.gitee.com/uploads/images/2022/0224/144027_e317f41f_1766278.png "屏幕截图.png")

### 更改 `Nacos` 自定义配置

**忠告: 微服务配置相当复杂 请勿在不懂原理的情况下乱改**

> `application.yml` 更改

![输入图片说明](https://images.gitee.com/uploads/images/2022/0224/144340_c91fbdad_1766278.png "屏幕截图.png")

> `datasource.yml` 更改

![输入图片说明](https://images.gitee.com/uploads/images/2022/0224/144507_4221d972_1766278.png "屏幕截图.png")

> `seata-server.properties` 更改

![输入图片说明](https://images.gitee.com/uploads/images/2022/0224/150013_f1f64f11_1766278.png "屏幕截图.png")

