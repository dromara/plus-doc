# RocketMQ 搭建
- - -

## 环境搭建

参考文章：

- [docker-compose 安装 RocketMQ 4.9.X (apache官方镜像) namesrv broker 与可视化控制台 console](https://lionli.blog.csdn.net/article/details/125798865)

补充说明：

- Cloud 示例中 RocketMQ 配置写在 `ruoyi-example/ruoyi-test-mq/src/main/resources/application.yml`。
- 默认示例使用 `name-server: localhost:9876`，生产环境请按实际集群地址调整。

## 用法参考

参考 `ruoyi-stream-mq` 模块测试案例：

![输入图片说明](https://foruda.gitee.com/images/1660031496623275622/屏幕截图.png "屏幕截图.png")

补充说明：

- 当前仓库中的实际示例模块为 `ruoyi-example/ruoyi-test-mq`。
- 可重点参考 `NormalRocketProducer`、`TransactionRocketProducer`、`NormalRocketConsumer`、`TransactionRocketConsumer`、`TranscationRocketListener`。
- 普通消息可通过 `/rocket/send` 测试，事务消息可通过 `/rocket/transaction` 测试。
- 使用前一般需要先在 RocketMQ 中创建对应的 `topic` 和 `group`。
