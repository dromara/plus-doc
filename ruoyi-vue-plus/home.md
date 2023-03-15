## 平台简介
[![码云Gitee](https://gitee.com/JavaLionLi/RuoYi-Vue-Plus/badge/star.svg?theme=blue)](https://gitee.com/JavaLionLi/RuoYi-Vue-Plus)
[![GitHub](https://img.shields.io/github/stars/JavaLionLi/RuoYi-Vue-Plus.svg?style=social&label=Stars)](https://github.com/JavaLionLi/RuoYi-Vue-Plus)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://gitee.com/JavaLionLi/RuoYi-Vue-Plus/blob/master/LICENSE)
[![使用IntelliJ IDEA开发维护](https://img.shields.io/badge/IntelliJ%20IDEA-提供支持-blue.svg)](https://www.jetbrains.com/?from=RuoYi-Vue-Plus)
<br>
[![RuoYi-Vue-Plus](https://img.shields.io/badge/RuoYi_Vue_Plus-5.0.0-success.svg)](https://gitee.com/JavaLionLi/RuoYi-Vue-Plus)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.0-blue.svg)]()
[![JDK-17](https://img.shields.io/badge/JDK-17-green.svg)]()
[![JDK-19](https://img.shields.io/badge/JDK-19-green.svg)]()

> RuoYi-Vue-Plus 是重写 RuoYi-Vue 针对 `分布式集群与多租户` 场景全方位升级(不兼容原框架)

> 项目代码、文档 均开源免费可商用 遵循开源协议在项目中保留开源协议文件即可<br>
活到老写到老 为兴趣而开源 为学习而开源 为让大家真正可以学到技术而开源

| 功能介绍     | 使用技术                | 文档地址                                                                                              | 特性注意事项                     |
|----------|---------------------|---------------------------------------------------------------------------------------------------|----------------------------|
| 当前框架     | RuoYi-Vue-Plus      | [RuoYi-Vue-Plus文档](https://gitee.com/JavaLionLi/RuoYi-Vue-Plus/wikis/pages)                       | 重写RuoYi-Vue全方位升级(不兼容原框架)   |
| 微服务分支    | RuoYi-Cloud-Plus    | [微服务分支地址](https://gitee.com/JavaLionLi/RuoYi-Cloud-Plus)                                          | 重写RuoYi-Cloud全方位升级(不兼容原框架) |
| 原框架      | RuoYi-Vue           | [RuoYi-Vue官网](http://ruoyi.vip/)                                                                  | 定期同步需要的功能                  |
| 前端开发框架   | Vue3、Element Plus   | [Element Plus官网](https://element-plus.org/zh-CN/#/zh-CN)                                          |                            |
| 后端开发框架   | SpringBoot          | [SpringBoot官网](https://spring.io/projects/spring-boot/#learn)                                     |                            |
| 容器框架     | Undertow            | [Undertow官网](https://undertow.io/)                                                                | 基于 XNIO 的高性能容器             |
| 权限认证框架   | Sa-Token、Jwt        | [Sa-Token官网](https://sa-token.dev33.cn/)                                                          | 强解耦、强扩展                    |
| 关系数据库    | MySQL               | [MySQL官网](https://dev.mysql.com/)                                                                 | 适配 8.X 最低 5.7              |
| 关系数据库    | Oracle              | [Oracle官网](https://www.oracle.com/cn/database/)                                                   | 适配 11g 12c                 |
| 关系数据库    | PostgreSQL          | [PostgreSQL官网](https://www.postgresql.org/)                                                       | 适配 13 14                   |
| 关系数据库    | SQLServer           | [SQLServer官网](https://docs.microsoft.com/zh-cn/sql/sql-server)                                    | 适配 2017 2019               |
| 缓存数据库    | Redis               | [Redis官网](https://redis.io/)                                                                      | 适配 6.X 最低 4.X              |
| 数据库框架    | Mybatis-Plus        | [Mybatis-Plus文档](https://baomidou.com/guide/)                                                     | 快速 CRUD 增加开发效率             |
| 数据库框架    | p6spy               | [p6spy官网](https://p6spy.readthedocs.io/)                                                          | 更强劲的 SQL 分析                |
| 多数据源框架   | dynamic-datasource  | [dynamic-ds文档](https://www.kancloud.cn/tracy5546/dynamic-datasource/content)                      | 支持主从与多种类数据库异构              |
| 序列化框架    | Jackson             | [Jackson官网](https://github.com/FasterXML/jackson)                                                 | 统一使用 jackson 高效可靠          |
| Redis客户端 | Redisson            | [Redisson文档](https://github.com/redisson/redisson/wiki/%E7%9B%AE%E5%BD%95)                        | 支持单机、集群配置                  |
| 分布式限流    | Redisson            | [Redisson文档](https://github.com/redisson/redisson/wiki/%E7%9B%AE%E5%BD%95)                        | 全局、请求IP、集群ID 多种限流          |
| 分布式队列    | Redisson            | [Redisson文档](https://github.com/redisson/redisson/wiki/%E7%9B%AE%E5%BD%95)                        | 普通队列、延迟队列、优先队列 等           |
| 分布式锁     | Lock4j              | [Lock4j官网](https://gitee.com/baomidou/lock4j)                                                     | 注解锁、工具锁 多种多样               |
| 分布式幂等    | Redisson            | [Lock4j文档](https://gitee.com/baomidou/lock4j)                                                     | 拦截重复提交                     |
| 分布式链路追踪  | Apache SkyWalking   | [Apache SkyWalking文档](https://skywalking.apache.org/docs/)                                        | 链路追踪、网格分析、度量聚合、可视化         |
| 分布式任务调度  | Xxl-Job             | [Xxl-Job官网](https://www.xuxueli.com/xxl-job/)                                                     | 高性能 高可靠 易扩展                |
| 文件存储     | Minio               | [Minio文档](https://docs.min.io/)                                                                   | 本地存储                       |
| 文件存储     | 七牛、阿里、腾讯            | [OSS使用文档](https://gitee.com/JavaLionLi/RuoYi-Vue-Plus/wikis/pages?sort_id=4359146&doc_id=1469725) | 云存储                        |
| 短信模块     | 阿里、腾讯               | [短信使用文档](https://gitee.com/JavaLionLi/RuoYi-Vue-Plus/wikis/pages?sort_id=5578491&doc_id=1469725)  | 短信发送                       |
| 监控框架     | SpringBoot-Admin    | [SpringBoot-Admin文档](https://codecentric.github.io/spring-boot-admin/current/)                    | 全方位服务监控                    |
| 校验框架     | Validation          | [Validation文档](https://docs.jboss.org/hibernate/stable/validator/reference/en-US/html_single/)    | 增强接口安全性、严谨性 支持国际化          |
| Excel框架  | Alibaba EasyExcel   | [EasyExcel文档](https://www.yuque.com/easyexcel/doc/easyexcel)                                      | 性能优异 扩展性强                  |
| 文档框架     | SpringDoc、javadoc   | [接口文档](https://gitee.com/JavaLionLi/RuoYi-Vue-Plus/wikis/pages?sort_id=5805266&doc_id=1469725)    | 无注解零入侵基于java注释             |
| 工具类框架    | Hutool、Lombok       | [Hutool文档](https://www.hutool.cn/docs/)                                                           | 减少代码冗余 增加安全性               |
| 代码生成器    | 适配MP、SpringDoc规范化代码 | [代码生成文档](https://gitee.com/JavaLionLi/RuoYi-Vue-Plus/wikis/pages?sort_id=5522329&doc_id=1469725)  | 一键生成前后端代码                  |
| 部署方式     | Docker              | [Docker文档](https://docs.docker.com/)                                                              | 容器编排 一键部署业务集群              |
| 国际化      | SpringMessage       | [SpringMVC文档](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc)   | Spring标准国际化方案              |

