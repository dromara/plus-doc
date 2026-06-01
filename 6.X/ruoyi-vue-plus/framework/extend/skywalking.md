# SkyWalking 链路监控
- - -

## 服务搭建

参考文章：

- https://lionli.blog.csdn.net/article/details/127656534

补充说明：

- SkyWalking 适合用来观察请求链路、调用耗时、异常分布与服务拓扑。
- 如果只是单机本地调试，优先确认应用本身能正常启动，再考虑引入链路探针，避免把问题复杂化。

## 代码改动

参考该提交开启相关注释：

- https://gitee.com/dromara/RuoYi-Vue-Plus/commit/4d02466fed4f3ea012a80c3359cde9af0737141f

补充说明：

- 老版本文档里很多地方是通过“打开注释”接入的，实际落地时要结合当前项目版本重新核对依赖和启动参数，不要机械照搬旧提交。
- 接入链路探针后，一般还要补充 JVM 启动参数，把 `skywalking-agent.jar` 正确挂载到应用进程。

## 本地使用

参考上方文章。

补充说明：

- 本地调试通常最关键的是确认 `agent.service_name`、`collector backend` 地址、应用启动脚本是否正确。
- 如果应用启动后监控平台没有数据，优先检查探针路径、端口联通性和服务名配置。

## Docker 部署

将 `agent` 探针放入服务器目录 `/docker/skywalking/agent/` 并授权。

![输入图片说明](https://foruda.gitee.com/images/1669032573170837535/d9901f53_1766278.png "屏幕截图")

补充说明：

- 容器部署时除了挂载 agent 目录，还要把 JVM 启动参数一并注入容器启动命令，否则只复制文件不会生效。
