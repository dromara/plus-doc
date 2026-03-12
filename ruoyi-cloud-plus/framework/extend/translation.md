# 翻译功能
- - -

## 版本

- >= 1.6.0

## 引入依赖

```xml
<dependency>
    <groupId>com.ruoyi</groupId>
    <artifactId>ruoyi-common-translation</artifactId>
</dependency>
```

## 注解说明

`@Translation`：标注在实体字段上，用于声明需要翻译的字段。  
`@TranslationType`：标注在实现类上，与 `@Translation` 的 `type` 一致，用于实现翻译逻辑。

![输入图片说明](https://foruda.gitee.com/images/1675575648043199227/d04b3e21_1766278.png "屏幕截图")

## 使用说明

**注意：翻译功能基于序列化实现，仅适合小数据量场景，不适用于 Excel 等大数据量导出。**  
建议缓存翻译结果，减少重复查询。

内置翻译类型：

- 用户 ID -> 账号/用户名
- 部门 ID -> 部门名称
- 字典 type -> label
- OSS ID -> URL

示例说明：

- 映射翻译：根据另一个字段映射到当前字段
- 直接翻译：根据当前字段直接替换
- 其他条件翻译：基于 `other` 自定义条件

![输入图片说明](https://foruda.gitee.com/images/1675575977860232549/143b74f8_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1675576044011477847/13eb9f57_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1675576265894720924/70792f66_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1675576391012282823/f95c5d78_1766278.png "屏幕截图")

## 自定义扩展

实现 `TranslationInterface` 并标注 `@TranslationType`，可参考框架默认实现。

![输入图片说明](https://foruda.gitee.com/images/1676735454308997001/cfcf3590_1766278.png "屏幕截图")
