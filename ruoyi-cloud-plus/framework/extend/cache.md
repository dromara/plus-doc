# 缓存说明
- - -
## 操作Redis缓存

框架采用 `redisson` 操作redis相关功能 提供了 `RedisUtils` 工具类 基本满足redis所有功能的使用

具体功能查看工具类方法 工具类不存在的方法可 `getClient()` 获取redisson客户端原生使用

## 多级缓存注解

框架采用spring自带的spring-cache注解体系 基于 Caffeine + Redis 实现多级缓存实现本地与redis双缓存存储

注解具体使用方式参考demo `RedisCacheController` 内含所有注解的使用方式

注解书写规则 可参考 `CacheNames` 代码注释说明用法

key 格式为 cacheNames#ttl#maxIdleTime#maxSize#local

* ttl 过期时间 如果设置为0则不过期 默认为0
* maxIdleTime 最大空闲时间 根据LRU算法清理空闲数据 如果设置为0则不检测 默认为0
* maxSize 组最大长度 根据LRU算法清理溢出数据 如果设置为0则无限长 默认为0
* local 默认开启本地缓存为1 关闭本地缓存为0

例子: test#60s、test#0#60s、test#0#1m#1000、test#1h#0#500、test#1h#0#500#0

**注意: 相同缓存的key必须一致 禁止出现同一个缓存 key与后方的参数不同这样会导致出现异常问题**

### 多级缓存工具类说明

框架针对注解不方便的接入的需求比较灵活的地方 但又需要使用注解或者与注解联动的需求 提供了 `CacheUtils` 工具类

工具类用于与spring-cache注解体系进行联动交互 禁止单独使用该工具当作redis工具类使用


