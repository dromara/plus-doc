# 主键使用说明
- - -

## 分布式 ID / 雪花 ID

框架默认集成雪花 ID，如需自定义可修改 `MybatisPlusConfig` 的 Bean。

![输入图片说明](https://foruda.gitee.com/images/1678979401707903546/e25f6c06_1766278.png "屏幕截图")

全局修改主键类型即可切换：

![输入图片说明](https://foruda.gitee.com/images/1678979411517764918/1470df04_1766278.png "屏幕截图")

如单表使用，可在实体上单独配置注解：

![输入图片说明](https://foruda.gitee.com/images/1678979416033986923/2a4c3736_1766278.png "屏幕截图")

## 注意事项

- 雪花 ID 位数较长，`Long` 在前端可能失真
- 框架已配置序列化方案，超出 JS 最大值自动转字符串
- 参考 `BigNumberSerializer` 类
