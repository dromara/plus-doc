# 多数据源
- - -

## 默认数据库与依赖

框架默认使用 `MySQL`。如需使用其他数据库，请在 `ruoyi-admin` 模块的 `pom.xml` 中增加对应 JDBC 依赖。

![输入图片说明](https://foruda.gitee.com/images/1721098535176969987/d42870ca_1766278.png "屏幕截图")

补充说明：

- 当前项目的多数据源配置位于各环境配置文件 `application-*.yml` 中的 `spring.datasource.dynamic`。
- 默认主数据源名称为 `master`，并开启了 `strict: true`，即匹配不到数据源时会直接报错。

## 多数据源事务

多数据源事务处理请参考 [事务相关](/ruoyi-vue-plus/framework/explain/transaction.md)。

## 功能概览

多数据源框架官方文档：[dynamic-datasource](https://www.kancloud.cn/tracy5546/dynamic-datasource/2264611)

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

## 用法说明

数据源加载顺序：`方法 > 类 > 默认`

![输入图片说明](https://foruda.gitee.com/images/1678979069737596299/abe8ae7f_1766278.png "屏幕截图")

补充说明：

- 最常见的用法是在 Service 或 Mapper 方法上加 `@DS("数据源名")`。
- 当前项目生成器模块已经使用了 `@DS("#dataName")` 这类 SpEL 写法，根据参数动态切换数据源。
- 新增数据源后，`@DS` 中填写的名称必须和配置里的数据源 key 完全一致。

## 配置示例

![输入图片说明](https://foruda.gitee.com/images/1678979074000345758/b9238f0b_1766278.png "屏幕截图")

补充说明：

- 如果只是增加一个只读库或业务库，通常只需要补充新的 `datasource.xxx` 配置，并在对应方法上标记 `@DS("xxx")`。
- 如果后续要接入 Seata，请同时关注动态数据源代理与 Seata 配置是否一致。

## 异构数据库

示例：`MySQL + Oracle`。具体配置请参考官方文档。

![输入图片说明](https://foruda.gitee.com/images/1678979078387192317/2de94a78_1766278.png "屏幕截图")
