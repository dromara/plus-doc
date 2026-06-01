# Nacos 集群搭建
- - -

## 集群搭建方式

### 1. 文件寻址

- [学习笔记 02 - Nacos（二）寻址机制之文件寻址分析](https://blog.csdn.net/Michelle_Zhong/article/details/127423521)

补充说明：

- 文件寻址适合节点数固定、机器变更较少的场景。
- 如果只是本地开发或测试环境，单机 Nacos 已经够用，不必一开始就上集群。

### 2. 地址服务器寻址（推荐）

- [学习笔记 03 - Nacos（三）使用 Nginx 实现地址服务器寻址及其原理分析](https://blog.csdn.net/Michelle_Zhong/article/details/127474238)

补充说明：

- 对 Cloud 项目更推荐通过统一代理地址接入 Nacos，便于后续扩容、迁移和故障切换。
- 当前项目中的 `spring.cloud.nacos.server-addr` 只需要填写代理后的 `ip:端口` 即可。

## 集群路由代理设置

- [学习笔记 04 - Nacos（四）使用 Nginx 简单实现 Nacos 集群负载均衡](https://blog.csdn.net/Michelle_Zhong/article/details/127486350)

设置好代理之后，后端 Nacos 地址直接使用代理 `ip:端口` 即可。

补充说明：

- Cloud 项目通常需要同时依赖 Nacos 的 `discovery` 和 `config` 能力，所以代理地址配置好后，两边都会共用同一套接入点。
- 除了 `server-addr`，还要同步确认 `namespace`、`group`、`username`、`password` 是否与实际环境一致。
