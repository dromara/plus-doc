# 5.X项目初始化
- - -

## 分支选择

| 分支       | 用途   | 说明             |
|----------|------|----------------|
| 5.X      | 稳定发布 | 推荐生产与学习        |
| dev      | 开发分支 | 代码随时更新，不建议直接使用 |
| future/* | 预览分支 | 新功能预览，稳定性不保证   |

## 运行环境清单
> 推荐使用 `Docker` 安装，项目内置编排文件。

**注意：禁止使用 `OracleJDK`（已知会导致 Spring 打包/运行异常）**

![输入图片说明](https://foruda.gitee.com/images/1720080025744223375/0213a652_1766278.png "屏幕截图")

| 组件            | 版本建议         | 说明                     |
|---------------|--------------|------------------------|
| JDK           | 17 / 21      | 推荐 OpenJDK（如 BellSoft） |
| MySQL         | 5.7 / 8.0    | 其他版本未测试，可反馈            |
| Oracle        | >= 12c       | 其他版本未测试，可反馈            |
| PostgreSQL    | 13 / 14 / 15 | 其他版本未测试，可反馈            |
| SQL Server    | 2017 / 2019  | 其他版本未测试，可反馈            |
| Redis         | >= 6.x       | 框架大量使用新特性              |
| MinIO         | 按需           | 可用 RustFS 替代（新方案需谨慎）   |
| Maven         | >= 3.8.x     | 构建工具                   |
| Node.js       | >= 20.15     | 其他版本未测试，可反馈            |
| npm           | >= 8.x       | 7.x 已确认存在问题            |
| IntelliJ IDEA | 见下方          | 有版本避坑说明                |


## IntelliJ IDEA 版本建议

- 2023 全系列不推荐（问题较多）
- 2024.1 / 2024.2：Maven 插件无法刷新依赖
- 2025.1 / 2025.2：存在已知问题
- 推荐使用：2024.3（JDK17）或 2025.3（JDK21-25）

## 搭建视频

[RuoYi-Vue-Plus 5.0 搭建与运行](https://www.bilibili.com/video/BV1Fg4y137JK/)

## 初始化步骤

### 1. 勾选 Maven 对应环境
![输入图片说明](https://foruda.gitee.com/images/1678976284045210056/a2f28d33_1766278.png "屏幕截图")

### 2. 确认 JDK 版本与配置
默认使用 `JDK17`，如需变更请同步修改项目配置。

![输入图片说明](https://foruda.gitee.com/images/1678941027820943505/c688e01e_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678941120518807034/4d56fcc9_1766278.png "屏幕截图")

### 3. 导入数据库 SQL
请按顺序依次导入，默认使用 `MySQL`。  
如需使用其他数据库，请参考 [多数据库数据源](/ruoyi-vue-plus/framework/extend/dynamic_datasource.md)。

![输入图片说明](https://foruda.gitee.com/images/1726304546467780078/b78cabd4_1766278.png "屏幕截图")

### 4. 配置主服务
在已勾选的环境配置文件中填写数据库与 Redis 配置。

![输入图片说明](https://foruda.gitee.com/images/1678941357316005626/70559736_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678941405169571070/0d06a955_1766278.png "屏幕截图")

其他数据库配置可按系统自带模板进行调整。

![输入图片说明](https://foruda.gitee.com/images/1678941444707120259/b274592a_1766278.png "屏幕截图")

### 5. 启动顺序与建议

必启基础服务：`MySQL`、`Redis`、`Admin`  
可选基础服务：`MinIO`（文件上传）、`Monitor`（监控）、`SnailJob`（定时任务）

![输入图片说明](https://foruda.gitee.com/images/1716175484919688429/8b9a79b7_1766278.png "屏幕截图")

- `MonitorAdminApplication`：Admin 监控服务  
- `SnailJobServerApplication`：任务调度中心服务  
- `DromaraApplication`：主应用服务

> 建议先启动 `MonitorAdminApplication` 与 `SnailJobServerApplication`，最后启动 `DromaraApplication`。  
> 工作流相关初始化请参考 [工作流初始化](/ruoyi-vue-plus/quickstart/worker_init.md)。

## 示例：最小化启动

仅体验基础功能时，可先启动 `MySQL`、`Redis` 与 `DromaraApplication`，其余服务按需再补充。
