# 关于如何使用分布式id或雪花id

### 3.5.0 版本

参考 `MybatisPlusConfig` 如需自定义 修改 `Bean` 实现即可

![输入图片说明](https://images.gitee.com/uploads/images/2021/1222/173238_e1fd816d_1766278.png "屏幕截图.png")

框架默认集成 雪花ID 只需全局更改 主键类型即可

![输入图片说明](https://images.gitee.com/uploads/images/2021/1222/173402_792b7103_1766278.png "屏幕截图.png")

如单表使用 可单独配置注解

![输入图片说明](https://images.gitee.com/uploads/images/2021/1222/173505_e212fa92_1766278.png "屏幕截图.png")

### 重点说明
* 由于雪花id位数过长 `Long` 类型在前端会失真
* 框架已配置序列化方案 超越 `JS` 最大值自动转字符串 参考 `BigNumberSerializer` 类 (3.0.0 及以上新增)
* 老版本处理方案
* 数据库使用 `varchar` 类型
* 在 `vo` 实体 使用 `@JsonSerialize(using = ToStringSerializer.class)` 序列化注解 转换为 `String` 类型