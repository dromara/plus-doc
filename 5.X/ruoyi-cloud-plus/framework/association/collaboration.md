# 多团队开发
- - -

## 推荐模式

多团队开发常见问题：请求被负载均衡到他人服务，导致调试困难。

建议模式：

- 使用一台测试机部署公共服务
- 本地只启动 `ruoyi-gateway` 与当前开发的业务模块
- 所有服务统一指向同一个 Nacos
- 前端指向本机 `ruoyi-gateway` 进行调试

## 负载均衡锁定

框架提供 `ruoyi-common-loadbalancer`，可将网关请求锁定到与网关相同 IP 的服务。

需在以下模块引入：

- `ruoyi-gateway`
- `ruoyi-auth`
- `ruoyi-modules`

![输入图片说明](https://foruda.gitee.com/images/1678980590168990366/afa2fdf6_1766278.png "屏幕截图")

请求转发与 RPC 调用时，会优先选择与本机 IP 相同的服务，找不到时才随机。

## 注意事项

- 检查本机是否存在虚拟网卡，避免 IP 识别错误
- 可使用以下代码检查本机 IP：

```java
InetAddress.getLocalHost().getHostAddress()
```
