### 关于多数据源事务 具体参考 `事务相关` 文档说明

### 多数据源框架功能介绍
多数据源框架官方文档: [dynamic-datasource文档](https://www.kancloud.cn/tracy5546/dynamic-datasource/2264611)

* 支持 数据源分组 ，适用于多种场景 纯粹多库 读写分离 一主多从 混合模式。
* 支持数据库敏感配置信息 加密 ENC()。
* 支持每个数据库独立初始化表结构schema和数据库database。
* 支持无数据源启动，支持懒加载数据源（需要的时候再创建连接）。
* 支持 自定义注解 ，需继承DS(3.2.0+)。
* 提供并简化对Druid，HikariCp，BeeCp，Dbcp2的快速集成。
* 提供对Mybatis-Plus，Quartz，ShardingJdbc，P6sy，Jndi等组件的集成方案。
* 提供 自定义数据源来源 方案（如全从数据库加载）。
* 提供项目启动后 动态增加移除数据源 方案。
* 提供Mybatis环境下的 纯读写分离 方案。
* 提供使用 spel动态参数 解析数据源方案。内置spel，session，header，支持自定义。
* 支持 多层数据源嵌套切换 。（ServiceA >>> ServiceB >>> ServiceC）。
* 提供 基于seata的分布式事务方案。
* 提供 本地多数据源事务方案。 附：不能和原生spring事务混用。

### 用法说明
加载顺序 `方法 => 类 => 默认`<br>
![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/213757_821f616d_1766278.png "屏幕截图.png")

### 配置方式
![输入图片说明](https://images.gitee.com/uploads/images/2021/1221/145455_f924ca42_1766278.png "屏幕截图.png")

### 数据库异构
例如: `mysql + oracle` 参考对应多数据源框架文档 [dynamic-ds文档](https://www.kancloud.cn/tracy5546/dynamic-datasource)
![输入图片说明](https://images.gitee.com/uploads/images/2021/1221/151102_0f1c90fe_1766278.png "屏幕截图.png")
