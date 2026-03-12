# 缓存说明
- - -

## Redis 操作

框架基于 `Redisson` 操作 Redis，提供 `RedisUtils` 工具类。  
如需原生能力，可通过 `RedisUtils.getClient()` 获取 Redisson 客户端。

## 多级缓存注解

框架基于 Spring Cache，使用 **Caffeine + Redis** 实现多级缓存。  
注解示例可参考 demo 中 `RedisCacheController`。

`CacheNames` 中定义了 key 规则：

`cacheNames#ttl#maxIdleTime#maxSize#local`

参数说明：

- `ttl`：过期时间，`0` 表示不过期
- `maxIdleTime`：最大空闲时间（LRU 清理），`0` 表示不检测
- `maxSize`：组最大长度（LRU 清理），`0` 表示无限长
- `local`：是否启用本地缓存，`1` 开启，`0` 关闭

示例：

- `test#60s`
- `test#0#60s`
- `test#0#1m#1000`
- `test#1h#0#500`
- `test#1h#0#500#0`

**注意：相同缓存的 key 必须一致，禁止同一缓存使用不同参数。**

## CacheUtils 工具类

`CacheUtils` 用于与 Spring Cache 注解联动，不建议当作 Redis 工具类单独使用。
