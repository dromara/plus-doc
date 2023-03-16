# 数据脱敏
- - -
## 功能说明

系统使用 `Jackson` 序列化策略 对标注了 `Sensitive` 注解的属性进行脱敏处理

## 使用教程

> 使用注解标注需要脱敏的字段 选择对应的策略

![输入图片说明](https://images.gitee.com/uploads/images/2022/0527/105325_3740cbf1_1766278.png "屏幕截图.png")

> 可再 `SensitiveStrategy` 内自定义策略

![输入图片说明](https://images.gitee.com/uploads/images/2022/0527/105417_25916103_1766278.png "屏幕截图.png")

## 脱敏逻辑修改

> 系统使用通用接口处理是否需要脱敏 多个系统可以自定义不同的脱敏逻辑实现

![输入图片说明](https://images.gitee.com/uploads/images/2022/0527/105641_6d978f2a_1766278.png "屏幕截图.png")

> 系统默认处理逻辑为 非管理员脱敏 可自行修改默认实现

![输入图片说明](https://images.gitee.com/uploads/images/2022/0527/105819_1d32091c_1766278.png "屏幕截图.png")



