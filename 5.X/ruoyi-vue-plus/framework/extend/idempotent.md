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

- `@RepeatSubmit` 目前支持 `interval`、`timeUnit`、`message` 三个参数。
- 默认间隔是 `5000ms`，并且框架限制最小间隔不能小于 `1` 秒。
- `message` 支持国际化编码写法，例如 `{repeat.submit.message}`。

```java
@RepeatSubmit(interval = 2, timeUnit = TimeUnit.SECONDS, message = "{repeat.submit.message}")
```

实现说明：

- 防重 key 来自 `请求URI + token + 请求参数摘要`，最终存储在 Redis 中。
- 接口执行成功后会保留锁直到超时时间结束，确保有效时间内不能再次提交。
- 如果业务返回失败结果或抛出异常，框架会提前释放锁，避免误伤后续重试。
- `MultipartFile`、`HttpServletRequest`、`HttpServletResponse`、`BindingResult` 等对象会被自动过滤，不参与参数摘要计算。
