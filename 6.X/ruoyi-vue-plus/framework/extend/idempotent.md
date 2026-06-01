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

## 模块位置

防重提交由公共 Redis 模块提供：

```text
ruoyi-common/ruoyi-common-redis
```

核心类：

```text
annotation/RepeatSubmit.java
aspectj/RepeatSubmitAspect.java
config/IdempotentConfig.java
utils/RedisUtils.java
```

防重状态存储在 Redis 中。

## 使用方式

在 Controller 方法上标注 `@RepeatSubmit`：

```java
@RepeatSubmit
@PostMapping
public R<Void> add(@Validated @RequestBody DemoBo bo) {
    return toAjax(demoService.insertByBo(bo));
}
```

指定间隔和提示：

```java
@RepeatSubmit(interval = 2, timeUnit = TimeUnit.SECONDS, message = "{repeat.submit.message}")
@PostMapping
public R<Void> submit(@RequestBody DemoBo bo) {
    return R.ok();
}
```

注解参数：

| 参数 | 默认值 | 说明 |
| --- | --- | --- |
| `interval` | `5000` | 防重间隔 |
| `timeUnit` | `MILLISECONDS` | 时间单位 |
| `message` | `{repeat.submit.message}` | 重复提交提示，支持国际化编码 |

## 判定规则

`RepeatSubmitAspect` 会构建 Redis key：

```text
repeat_submit:{请求URI}:{token}:{请求参数摘要}
```

同一个用户在同一个接口提交相同参数，且 Redis key 未过期时，会抛出重复提交异常。

处理结果：

- 第一次提交成功写入 Redis，并设置过期时间。
- 接口成功返回时保留 key，直到超时自动释放。
- 接口抛异常时会删除 key，允许用户修正后重试。

## 使用注意

- `interval` 转换为毫秒后不能小于 `1000`。
- 防重只解决短时间重复点击、重复请求，不等同于业务幂等。
- 支付、订单、回调等强幂等场景仍应使用业务唯一键、状态机或数据库唯一约束。
- 只对经过 Spring AOP 代理的方法生效。
