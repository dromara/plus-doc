# 缓存说明
- - -

## Redis 操作

框架基于 `Redisson` 操作 Redis，提供 `RedisUtils` 工具类。  
如需原生能力，可通过 `RedisUtils.getClient()` 获取 Redisson 客户端。

补充说明：

- 当前 Redis 与 Redisson 的基础配置位于各环境配置文件中。
- 需要直接操作字符串、集合、分布式锁等原生 Redis 能力时，优先使用 `RedisUtils`。

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

补充说明：

- `local=1` 时表示开启本地缓存，一般是 `Caffeine + Redis` 两级缓存。
- `local=0` 时表示只使用远程缓存。
- 同一缓存组如果参数写法不统一，最终会造成缓存行为不一致，排查起来很麻烦。

## CacheUtils 工具类

`CacheUtils` 用于与 Spring Cache 注解联动，不建议当作 Redis 工具类单独使用。

补充说明：

- 如果某个业务已经用 `@Cacheable`、`@CachePut`、`@CacheEvict` 管理缓存，手动清理时也尽量配套使用 `CacheUtils`，避免跳过多级缓存体系只删了 Redis 没删本地缓存。
