# 邮件功能
- - -

## 模块位置

单体项目邮箱验证码接口在：

```text
ruoyi-admin/src/main/java/org/dromara/web/controller/CaptchaController.java
```

公共邮件能力：

```text
ruoyi-common/ruoyi-common-mail
org.dromara.common.mail.core.MailBuilder
```

## 配置位置

邮件配置位于环境配置文件：

```text
ruoyi-admin/src/main/resources/application-dev.yml
ruoyi-admin/src/main/resources/application-prod.yml
```

配置前缀：

```text
mail
```

`mail.enabled=false` 时验证码接口会直接返回未开启提示。

## 接口路径

验证码接口：

```text
GET /resource/email/code?email=邮箱地址
```

处理流程：

1. 检查 `mail.enabled`。
2. 校验邮箱格式。
3. 生成 4 位数字验证码。
4. 使用 `GlobalConstants.CAPTCHA_CODE_KEY + email` 写入 Redis。
5. 通过 `MailBuilder` 发送验证码邮件。

实际发送方法带有限流：

```java
@RateLimiter(key = "#email", time = 60, count = 1)
```

## 业务调用

```java
MailBuilder.of()
    .to("user@example.com")
    .subject("标题")
    .text("内容")
    .send();
```

`MailBuilder` 也支持 HTML 内容、抄送、密送、附件、内嵌图片等能力，按业务需要封装统一发送入口。

## 使用注意

- 邮箱服务商常使用授权码，不一定是登录密码。
- 验证码已写入 Redis，登录或校验时要使用同一 key 规则读取。
- 批量通知、营销邮件不建议直接复用验证码接口，应单独封装队列和重试机制。
