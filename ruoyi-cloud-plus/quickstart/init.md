# 2.X项目初始化
- - -

## 分支选择

| 分支       | 用途   | 说明             |
|----------|------|----------------|
| 2.X      | 稳定发布 | 推荐生产与学习        |
| dev      | 开发分支 | 代码随时更新，不建议直接使用 |
| future/* | 预览分支 | 新功能预览，稳定性不保证   |

## 运行环境清单
> 推荐使用 `Docker` 安装，项目内置编排文件。

**注意：禁止使用 `OracleJDK`（已知会导致 Spring 打包/运行异常）**

![输入图片说明](https://foruda.gitee.com/images/1720080025744223375/0213a652_1766278.png "屏幕截图")

| 组件         | 版本建议         | 说明                                                                       |
|------------|--------------|--------------------------------------------------------------------------|
| JDK        | 17 / 21      | 推荐 OpenJDK [JDK下载地址](https://bell-sw.com/pages/downloads/)               |
| MySQL      | 5.7 / 8.0    | 其他版本未测试，可反馈                                                              |
| Oracle     | >= 12c       | 其他版本未测试，可反馈                                                              |
| PostgreSQL | 13 / 14 / 15 | 其他版本未测试，可反馈                                                              |
| Redis      | >= 6.x       | 框架大量使用新特性 [win redis 下载地址](https://github.com/zkteco-home/redis-windows) |
| MinIO      | 按需           | 可用 RustFS 替代（新方案需谨慎）                                                     |
| Maven      | >= 3.8.x     | 构建工具                                                                     |
| Node.js    | >= 20.15     | 其他版本未测试，可反馈                                                              |
| npm        | >= 8.x       | 7.x 已确认存在问题                                                              |
| Nacos      | >= 2.x       | 建议使用框架内置版本                                                               |
| Sentinel   | 框架内置         | 建议使用框架内置版本                                                               |
| Seata      | 框架内置         | 建议使用框架内置版本                                                               |

## IntelliJ IDEA 版本建议

- 2023 全系列不推荐（问题较多）
- 2024.1 / 2024.2：Maven 插件无法刷新依赖
- 2025.1 / 2025.2：存在已知问题
- 推荐使用：2024.3（JDK17）或 2025.3（JDK21-25）

## 初始化步骤

### 1. 勾选 Maven 对应环境

![输入图片说明](https://foruda.gitee.com/images/1678976284045210056/a2f28d33_1766278.png "屏幕截图")

### 2. 确认 JDK 版本与配置

默认使用 `JDK17`，如需变更请同步修改项目配置。

![输入图片说明](https://foruda.gitee.com/images/1678941027820943505/c688e01e_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678941120518807034/4d56fcc9_1766278.png "屏幕截图")

### 3. 导入数据库 SQL

将 SQL 导入到与文件名对应的数据库（不要放到同一个库）。  
默认数据库为 `MySQL`，如需使用其他数据库请参考 [多数据库数据源](/ruoyi-cloud-plus/framework/extend/dynamic_datasource.md)。

![输入图片说明](https://foruda.gitee.com/images/1717122730708924506/7f3aaecf_1766278.png "屏幕截图")

### 4. Nacos 选择

#### 4.1 使用内置 `ruoyi-nacos`

修改 `ruoyi-nacos` 的数据库连接地址。

![输入图片说明](https://foruda.gitee.com/images/1664422006264405180/cac5afc6_1766278.png "屏幕截图")

后续流程与自建 Nacos 相同。

#### 4.2 自建 Nacos

**注意：自建 Nacos 必须与框架版本一致，Nacos 版本兼容性较差。**

**Nacos 数据库必须指向 `ry-config`（此库为定制配置库，不可替换）。**

将项目 `script/config/nacos` 下所有配置复制到 Nacos 中。  
建议手动复制内容，避免编码不一致导致解析问题。

**注意: 不懂就不要乱改配置文件内容 框架内所有功能都是配置好的!!!不要画蛇添足**<br>
**注意: 不懂就不要乱改配置文件内容 框架内所有功能都是配置好的!!!不要画蛇添足**<br>
**注意: 不懂就不要乱改配置文件内容 框架内所有功能都是配置好的!!!不要画蛇添足**<br>

![输入图片说明](https://foruda.gitee.com/images/1746693993121928066/26033bb1_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678979856705927770/75cc1e8c_1766278.png "屏幕截图")

更新主 `pom` 对应环境中的 Nacos 地址配置。

![输入图片说明](https://foruda.gitee.com/images/1678979881888833924/7e6a191f_1766278.png "屏幕截图")

### 5. 修改 Nacos 自定义配置

**忠告: 微服务配置相当复杂 请勿在不懂原理的情况下乱改**<br>
**忠告: 微服务配置相当复杂 请勿在不懂原理的情况下乱改**<br>
**忠告: 微服务配置相当复杂 请勿在不懂原理的情况下乱改**<br>

微服务配置较复杂，请确认理解后再修改。  
建议仅修改必要项，如数据库地址、Redis 地址、Seata 地址等。

- `application-common.yml`
- `datasource.yml`
- `seata-server.properties`

![输入图片说明](https://foruda.gitee.com/images/1678979889410167794/100db4ab_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678979894464784408/0d020c07_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678979902433843257/12da2839_1766278.png "屏幕截图")

### 6. 使用内置 `ruoyi-seata-server`

执行 `ry-seata.sql` 初始化 Seata 服务端数据库。  
修改 Nacos 中 `seata-server.properties` 的数据库地址。  
启动 `ruoyi-seata-server` 服务。

### 7. 服务启动顺序

必启基础服务：`MySQL`、`Redis`、`Nacos`  
可选基础服务：`MinIO`（文件上传）、`Seata`（分布式事务，默认开启）、`Sentinel`（熔断限流）、`Monitor`（监控）、`SnailJob`（定时任务）

必启应用服务：`Gateway`、`Auth`、`System`  
可选应用服务：`Resource`（资源、文件上传、邮件、短信）、`Workflow`（工作流）、`Gen`（代码生成）、`Job`（定时任务）、`Demo`（演示）
