# 实体 Bean 为空问题
- - -


## 问题现象

读取或转换实体时，字段值始终为空。


## 常见原因

实体使用了 `@Accessors(chain = true)`，导致 `set` 方法返回值为 `this`，与部分框架的标准 Java Bean 约定不兼容。

## 原因
java 规范 set 返回值为 `void` 链式调用 set 返回值为 `this`<br>
故多数框架底层使用 jdk 工具导致找不到 set 方法<br>
例如: `easyexcel` `cglib` `mybatis` 等

## 解决方案

1. 移除 `@Accessors(chain = true)`。
2. 重新编译并验证读取是否正常。

## 影响范围

易受影响的工具包含但不限于：`easyexcel`、`cglib`、`mybatis`。
