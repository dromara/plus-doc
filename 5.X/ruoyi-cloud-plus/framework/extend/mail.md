# 邮件功能
- - -

## 配置方式

在配置文件中开启邮件功能：

![输入图片说明](https://foruda.gitee.com/images/1663555260932007318/fabb2bfa_1766278.png "屏幕截图")

- `enabled`：邮件功能开关

补充说明：

- Cloud 版本邮件配置通常维护在 Nacos 的 `ruoyi-resource.yml` 中。
- 当前资源服务已经提供 `SysEmailController`，可直接用于邮箱验证码场景。
- 邮件验证码发送逻辑内部已配合 Redis 和限流注解做基础控制。

## 功能使用

参考 demo 模块 `MailController` 示例：

![输入图片说明](https://foruda.gitee.com/images/1663555374113593089/885b4db2_1766278.png "屏幕截图")

补充说明：

- Cloud 实际项目里更建议参考资源服务中的 `/resource/email/code` 接口用法，而不是只看旧的 demo 截图。
- 功能思路与 Vue 版本一致，可结合 [Vue 版本邮件功能说明](/ruoyi-vue-plus/framework/extend/mail.md) 一起看。
