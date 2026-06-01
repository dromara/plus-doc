# RabbitMQ 搭建
- - -

## 环境搭建

参考文章：

- [docker-compose 安装 RabbitMQ 3.X 附带延迟队列插件](https://lionli.blog.csdn.net/article/details/125855177)

补充说明：

- Cloud 示例中 RabbitMQ 配置写在 `ruoyi-example/ruoyi-test-mq/src/main/resources/application.yml`。
- 如果需要测试延迟消息，请确认 RabbitMQ 已正确安装延迟队列相关插件。

## 用法参考

参考 `ruoyi-stream-mq` 模块测试案例：

![输入图片说明](https://foruda.gitee.com/images/1660031371503504748/屏幕截图.png "屏幕截图.png")

补充说明：

- 当前仓库中的实际示例模块为 `ruoyi-example/ruoyi-test-mq`。
- 可重点参考 `NormalRabbitProducer`、`DelayRabbitProducer`、`RabbitConsumer`、`RabbitConfig`、`RabbitTtlQueueConfig`。
- 快速验证时，可访问 `/rabbit/send` 发送普通消息，访问 `/rabbit/sendDelay?delay=毫秒值` 发送延迟消息。
