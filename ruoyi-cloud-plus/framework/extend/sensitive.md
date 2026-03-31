# 数据脱敏
- - -

## 功能说明

系统基于 `Jackson` 序列化策略，对标注 `@Sensitive` 的字段进行脱敏处理。

补充说明：

- Cloud 版本与 Vue 版本共用同一套公共脱敏组件。
- 脱敏主要作用于接口响应序列化阶段，不会修改数据库原始值。

## 使用方式

在字段上标注 `@Sensitive`，并指定策略与权限：

![输入图片说明](https://foruda.gitee.com/images/1699523591703893602/ffd6dba2_1766278.png "屏幕截图")

字段说明：

- `strategy`：脱敏策略
- `roleKey`：角色 code（满足角色可查看明文）
- `perms`：权限 code（满足权限可查看明文）

![输入图片说明](https://foruda.gitee.com/images/1678979315796014155/614adf91_1766278.png "屏幕截图")

## 自定义脱敏策略

在 `SensitiveStrategy` 中新增策略实现：

![输入图片说明](https://foruda.gitee.com/images/1678979319996224858/3b3e3c8b_1766278.png "屏幕截图")

## 脱敏逻辑调整

可通过通用接口自定义脱敏逻辑，支持不同系统使用不同规则。

![输入图片说明](https://foruda.gitee.com/images/1678979325448998856/b262e425_1766278.png "屏幕截图")

默认逻辑：根据角色/权限或非管理员进行脱敏，可按需修改。

![输入图片说明](https://foruda.gitee.com/images/1699523752627488891/f82f2f50_1766278.png "屏幕截图")

补充说明：

- 使用方式与 Vue 版本一致，可直接参考 [Vue 版本数据脱敏说明](/ruoyi-vue-plus/framework/extend/sensitive.md)。
- Cloud 场景下只需要确保相关服务已引入公共脱敏组件并使用统一权限体系即可。
