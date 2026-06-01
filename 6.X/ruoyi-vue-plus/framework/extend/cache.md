# 缓存
- - -

## 模块位置

缓存能力由公共 Redis 模块提供：

```text
ruoyi-common/ruoyi-common-redis
```

核心类：

```text
utils/RedisUtils.java
utils/CacheUtils.java
manager/PlusSpringCacheManager.java
manager/CaffeineCacheDecorator.java
config/RedisConfig.java
config/CacheConfig.java
```

缓存名常量位于：

```text
ruoyi-common/ruoyi-common-core/src/main/java/org/dromara/common/core/constant/CacheNames.java
```

## RedisUtils

`RedisUtils` 是直接操作 Redis 的工具类，底层使用 Redisson：

```java
RedisUtils.setCacheObject("demo:key", value, Duration.ofMinutes(10));
DemoVo vo = RedisUtils.getCacheObject("demo:key");
RedisUtils.deleteObject("demo:key");
```

如需 Redisson 原生能力：

```java
RedissonClient client = RedisUtils.getClient();
```

## Spring Cache

项目使用自定义 `PlusSpringCacheManager`，基于 Redisson 实现 Spring Cache，并可叠加 Caffeine 本地缓存。

常用注解：

```java
@Cacheable(cacheNames = CacheNames.SYS_CONFIG, key = "#configKey")
public String selectConfigByKey(String configKey) {
    return mapper.selectConfig(configKey);
}

@CacheEvict(cacheNames = CacheNames.SYS_CONFIG, key = "#configKey")
public void clearConfig(String configKey) {
}
```

## 缓存名格式

`CacheNames` 约定格式：

```text
cacheNames#ttl#maxIdleTime#maxSize#local
```

参数含义：

| 参数 | 说明 |
| --- | --- |
| `ttl` | 过期时间，`0` 表示不过期 |
| `maxIdleTime` | 最大空闲时间，`0` 表示不检测 |
| `maxSize` | 缓存组最大长度，`0` 表示无限长 |
| `local` | 是否启用本地缓存，`1` 开启，`0` 关闭 |

示例：

```text
demo#60s
demo#0#60s
demo#0#1m#1000
demo#1h#0#500
demo#1h#0#500#0
```

## CacheUtils

`CacheUtils` 用于操作 Spring Cache 管理的缓存：

```java
CacheUtils.put(CacheNames.SYS_CONFIG, "key", value);
Object value = CacheUtils.get(CacheNames.SYS_CONFIG, "key");
CacheUtils.evict(CacheNames.SYS_CONFIG, "key");
```

它适合和 `@Cacheable`、`@CacheEvict` 使用同一套缓存名，不建议替代 `RedisUtils` 做通用 Redis 操作。

## 使用注意

- 同一个缓存名不要在不同位置使用不同参数。
- 启用本地缓存后，要注意缓存淘汰时机。
- 大对象、高频写对象不建议直接放入 Spring Cache。
- 通用 Redis 读写优先使用 `RedisUtils`，Spring Cache 联动场景使用 `CacheUtils`。
