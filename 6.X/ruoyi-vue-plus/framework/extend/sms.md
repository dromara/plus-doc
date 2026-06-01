# 短信模块
- - -

已完成 sms4j 集成，文档地址：https://sms4j.com/doc3/

## 模块位置

单体项目短信验证码接口在：

```text
ruoyi-admin/src/main/java/org/dromara/web/controller/CaptchaController.java
```

公共短信能力由 `sms4j` 提供：

```text
ruoyi-common/ruoyi-common-sms
```

## 配置位置

短信配置位于环境配置文件：

```text
ruoyi-admin/src/main/resources/application-dev.yml
ruoyi-admin/src/main/resources/application-prod.yml
```

`sms.blends` 下可以配置多个通道，代码通过配置 key 选择通道：

```java
SmsBlend smsBlend = SmsFactory.getSmsBlend("config1");
```

`config1` 必须和 `sms.blends` 下的 key 对应。

## 接口路径

验证码接口：

```text
GET /resource/sms/code?phoneNumber=手机号
```

处理流程：

1. 校验手机号格式。
2. 生成 4 位数字验证码。
3. 使用 `GlobalConstants.CAPTCHA_CODE_KEY + phoneNumber` 写入 Redis。
4. 通过 `SmsFactory.getSmsBlend("config1")` 获取通道。
5. 调用 `sendMessage(phoneNumber, templateId, map)` 发送短信。

接口带有限流：

```java
@RateLimiter(key = "#phonenumber", time = 60, count = 1)
```

## 业务调用

业务代码可直接使用 `SmsFactory`：

```java
LinkedHashMap<String, String> params = new LinkedHashMap<>();
params.put("code", "1234");

SmsBlend smsBlend = SmsFactory.getSmsBlend("config1");
SmsResponse response = smsBlend.sendMessage(phoneNumber, templateId, params);
```

## 使用注意

- 验证码模板 ID 当前示例为空，实际业务需要按供应商模板配置。
- 模板参数使用 `LinkedHashMap`，字段名和顺序按供应商要求填写。
- 验证码已写入 Redis，登录或校验时要使用同一 key 规则读取。
- 生产环境应配合限流、黑名单、图形验证码或滑块验证码，避免短信轰炸。
