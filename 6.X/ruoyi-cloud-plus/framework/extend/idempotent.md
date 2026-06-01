# 防重幂等
- - -

## 功能说明

防重用于避免短时间内重复提交导致数据污染。  
框架参考美团 GTIS 防重系统，通过请求参数 + 用户 Token/URL 生成全局业务 ID。  
可有效限制同一用户在限定时间内对同一业务提交相同数据。

说明：

- 业务失败或异常会快速释放限制
- 只对“同一用户 + 同一接口 + 相同数据”生效
- 与并发压测不是同一类问题

## 参考资料

[美团 分布式系统互斥性与幂等性问题的分析与解决](https://tech.meituan.com/2016/09/29/distributed-system-mutually-exclusive-idempotence-cerberus-gtis.html)

![输入图片说明](https://foruda.gitee.com/images/1678979231862359032/34f030c5_1766278.png "屏幕截图")

## 使用方法

在 Controller 上标注 `@RepeatSubmit`：

![输入图片说明](https://foruda.gitee.com/images/1678979236772683145/9fa27e5b_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678979240831458322/8e1fac4b_1766278.png "屏幕截图")

补充说明：

- Cloud 版本使用的也是公共幂等组件，注解参数、Redis 防重逻辑、成功/失败释放策略与 Vue 版本一致。
- `@RepeatSubmit` 支持 `interval`、`timeUnit`、`message`，默认间隔 `5000ms`，最小不能小于 `1` 秒。
- `message` 同样支持国际化编码写法，例如 `{repeat.submit.message}`。

```java
@RepeatSubmit(interval = 2, timeUnit = TimeUnit.SECONDS, message = "{repeat.submit.message}")
```

实现说明：

- 防重 key 由 `请求URI + token + 请求参数摘要` 组成并存入 Redis。
- 接口成功返回时会保留限制直到超时；失败或异常会立即释放，便于用户重试。
- 具体使用细节可直接参考 [Vue 版本说明](/ruoyi-vue-plus/framework/extend/idempotent.md)。
