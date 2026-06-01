# 缓存说明
- - -

## Redis 操作

框架基于 `Redisson` 操作 Redis，提供 `RedisUtils` 工具类。  
如需原生能力，可通过 `RedisUtils.getClient()` 获取 Redisson 客户端。

补充说明：

- Cloud 版本同样使用公共 Redis 组件，原生 Redis 操作方式与 Vue 版本一致。
- Redis 基础配置通常统一放在 Nacos 公共配置中，由各服务按需继承。

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

- 使用方式与 Vue 版本一致，可直接参考 [Vue 版本缓存说明](/ruoyi-vue-plus/framework/extend/cache.md)。
- 在微服务场景下，特别要避免不同服务对同一个缓存组写出不同的缓存参数。

## CacheUtils 工具类

`CacheUtils` 用于与 Spring Cache 注解联动，不建议当作 Redis 工具类单独使用。
