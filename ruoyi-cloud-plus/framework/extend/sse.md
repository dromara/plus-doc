# SSE功能
- - -

## 框架版本 >= 2.2.1

## 配置说明

配置在 `ruoyi-resource` 目录下 远程调用可直接使用 `RemoteMessageService` 接口

![输入图片说明](https://foruda.gitee.com/images/1721986989993234455/4214cbbd_1766278.png "屏幕截图")

* enabled 是否开启此功能
* path 应用路径

**重点: 如关闭ws功能需连同前端ws开关一同关闭 不然前端启动会报错**

![输入图片说明](https://foruda.gitee.com/images/1728971445611402828/06519718_1766278.png "屏幕截图")

## 使用方法

前端连接方式: `http://后端ip:端口/resource/sse?clientid=import.meta.env.VITE_APP_CLIENT_ID&Authorization=Bearer eyJ0eXAiO......`

其中 `Authorization` 为请求token需要登录后获取 连接成功之后 与框架内其他获取登录用户方式一致

`SseMessageUtils.sendMessage` 推送单机消息(特殊需求使用)<br>
`SseMessageUtils.subscribeMessage` 订阅分布式消息(框架初始化已订阅)<br>
`SseMessageUtils.publishMessage` 发布分布式消息(推荐使用 所有集群内寻找到接收人)<br>
`SseMessageUtils.publishAll` 群发消息给所有连接人<br>