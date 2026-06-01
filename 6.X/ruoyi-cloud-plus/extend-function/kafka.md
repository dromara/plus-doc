# Kafka 搭建
- - -

## 环境搭建

参考文章：

- [docker-compose 安装 Kafka 3.X 附带可视化界面](https://lionli.blog.csdn.net/article/details/125855550)

补充说明：

- Cloud 示例项目中 Kafka 配置写在 `ruoyi-example/ruoyi-test-mq/src/main/resources/application.yml`。
- 当前示例主要关注本地开发调试，默认 `bootstrap-servers` 为 `localhost:9092`。

## 用法参考

参考 `ruoyi-stream-mq` 模块测试案例：

![输入图片说明](https://foruda.gitee.com/images/1660031528265343174/屏幕截图.png "屏幕截图.png")

补充说明：

- 当前仓库中的实际示例模块为 `ruoyi-example/ruoyi-test-mq`。
- 可以直接参考其中的 `KafkaNormalProducer`、`KafkaNormalConsumer` 和 `PushMessageController`。
- 快速验证时，可启动示例服务后访问 `/kafka/send` 发送测试消息。
