# WebSocket功能
- - -

## 框架版本 >= 2.0.0

## 配置说明

![输入图片说明](https://foruda.gitee.com/images/1688356273985385949/5e4d1de8_1766278.png "屏幕截图")

* enabled 是否开启此功能
* path 应用路径
* allowedOrigins 设置访问源地址

## 使用方法

前端连接方式: `ws://localhost/websocket?Authorization=Bearer eyJ0eXAiO......`

**由于js不支持请求头传输故而采用参数传输 如支持请求头传输建议使用请求头传输**

其中 `Authorization` 为请求token需要登录后获取 连接成功之后 与框架内其他获取登录用户方式一致

`WebSocketUtils.sendMessage` 发布单机消息(特殊需求使用)<br>
`WebSocketUtils.subscribeMessage` 订阅分布式消息(框架初始化已订阅)<br>
`WebSocketUtils.publishMessage` 发布分布式消息(建议使用支持集群分布式消息同步)<br>