# 参数校验
- - -

参数校验基于 `spring-boot-starter-validation` 与 `hibernate-validator`，用于对请求参数进行统一校验。

## 基础用法

### 方法一：使用 `@Validated`

步骤建议：

1. 在类或方法参数上标注 `@Validated`

```java
@Validated
@RestController
@RequestMapping("/auth")
public class AuthController {

    @PostMapping("/login")
    public R<LoginVo> login(@RequestBody LoginBody body) {
        // ...
    }
}
```

```java
@PostMapping
public R<Void> add(@Validated @RequestBody SysUserBo user) {
    // ...
}
```

补充说明：
- 类上加 `@Validated` 适合统一开启方法参数校验
- 参数上加 `@Validated` 适合只校验当前请求体
- 代码生成器默认也会在新增、修改、查询等场景生成对应校验写法

2. 在对象字段上添加校验注解

```java
public class SysUserBo {

    @NotBlank(message = "用户账号不能为空")
    @Size(min = 0, max = 30, message = "用户账号长度不能超过{max}个字符")
    private String userName;

    @NotBlank(message = "用户昵称不能为空")
    @Size(min = 0, max = 30, message = "用户昵称长度不能超过{max}个字符")
    private String nickName;

    @Email(message = "邮箱格式不正确")
    @Size(min = 0, max = 50, message = "邮箱长度不能超过{max}个字符")
    private String email;
}
```

_注：message 支持 EL 表达式，`{max}` 会读取注解中的参数值。_

### 方法二：使用工具类 `ValidatorUtils`

`org.dromara.common.core.utils.ValidatorUtils`

![输入图片说明](https://foruda.gitee.com/images/1700050047426137432/206bd032_4959041.png "屏幕截图")

常用方式：

```java
// 校验所有带有校验注解的属性
ValidatorUtils.validate(object);
```

```java
// 按分组校验（可传多个分组）
ValidatorUtils.validate(object, group);
```

这种方式更适合非 Controller 场景，例如定时任务、消息消费、组装对象后的二次校验。

## 扩展用法

### 自定义校验注解

可基于业务实现自定义注解。以下以 `@Xss` 为例：

```java
@Xss(message = "用户账号不能包含脚本字符")
@NotBlank(message = "用户账号不能为空")
@Size(min = 0, max = 30, message = "用户账号长度不能超过{max}个字符")
private String userName;
```

步骤建议：

1. 新增注解：`org.dromara.common.core.xss.Xss`

![输入图片说明](https://foruda.gitee.com/images/1700048074014527096/b4e230c2_4959041.png "屏幕截图")

2. 实现校验器：`org.dromara.common.core.xss.XssValidator`

![输入图片说明](https://foruda.gitee.com/images/1700048474563719650/f9172bdc_4959041.png "屏幕截图")

### 分组校验

适用于“新增/更新字段校验不同”的场景。

步骤建议：

1. 自定义分组接口

![输入图片说明](https://foruda.gitee.com/images/1700049439236073123/9e0d2e16_4959041.png "屏幕截图")

2. 在 `@Validated` 指定分组

![输入图片说明](https://foruda.gitee.com/images/1700049302803077030/c2a985aa_4959041.png "屏幕截图")

3. 在字段注解中设置分组

![输入图片说明](https://foruda.gitee.com/images/1700049205699437759/96babbd6_4959041.png "屏幕截图")

框架中常见分组：
- `AddGroup`：新增
- `EditGroup`：修改
- `QueryGroup`：查询条件校验

如果某个字段只在新增时必填，不应直接写成无分组 `@NotBlank`，否则修改接口也会被一并限制。

## 附录：常用校验注解

| 注解               | 使用（只列举特殊参数值）                         | 参数类型                                          | 说明               |
|------------------|--------------------------------------|-----------------------------------------------|------------------|
| @AssertFalse     | @AssertFalse                         | boolean / Boolean                             | 元素值必须为 false     |
| @AssertTrue      | @AssertTrue                          | boolean / Boolean                             | 元素值必须为 true      |
| @DecimalMax      | @DecimalMax(value=值)                 | BigDecimal / BigInteger / CharSequence / 数字类型 | 元素必须 <= 指定最大值    |
| @DecimalMin      | @DecimalMin(value=值)                 | BigDecimal / BigInteger / CharSequence / 数字类型 | 元素必须 >= 指定最小值    |
| @Digits          | @Digits(integer=整数位值, fraction=小数位值) | BigDecimal / BigInteger / CharSequence / 数字类型 | 元素必须符合整数/小数位范围   |
| @Email           | @Email(regexp=正则表达式, flags=标志)       | CharSequence                                  | 元素是否符合正则表达式      |
| @Future          | @Future                              | 同 @Future                                     | 元素必须是未来的时刻/日期/时间 |
| @FutureOrPresent | @FutureOrPresent                     | 同 @Future                                     | 元素必须是当前或未来       |
| @Length          | @Length(min=最小值, max=最大值)            | CharSequence                                  | 验证字符串长度范围        |
| @Max             | @Max(value=值)                        | BigDecimal / BigInteger / 数字类型                | 元素必须 <= 指定最大值    |
| @Min             | @Min(value=值)                        | BigDecimal / BigInteger / 数字类型                | 元素必须 >= 指定最小值    |
| @Negative        | @Negative                            | BigDecimal / BigInteger / 数字类型                | 元素必须为严格负数        |
| @NegativeOrZero  | @NegativeOrZero                      | BigDecimal / BigInteger / 数字类型                | 元素必须为负数或 0       |
| @NotBlank        | @NotBlank                            | CharSequence                                  | 元素不能为空白字符串       |
| @NotEmpty        | @NotEmpty                            | CharSequence / Collection / Map / Array       | 元素不能为空或空集合       |
| @NotNull         | @NotNull                             | 不限类型                                          | 元素不能为 null       |
| @Null            | @Null                                | 不限类型                                          | 元素必须为 null       |
| @Past            | @Past                                | 同 @Future                                     | 元素必须是过去的时刻/日期/时间 |
| @PastOrPresent   | @PastOrPresent                       | 同 @Future                                     | 元素必须是过去或现在       |
| @Pattern         | @Pattern(regexp=正则表达式, flags=标志)     | CharSequence                                  | 元素必须匹配正则表达式      |
| @Positive        | @Positive                            | BigDecimal / BigInteger / 数字类型                | 元素必须为严格正数        |
| @PositiveOrZero  | @PositiveOrZero                      | BigDecimal / BigInteger / 数字类型                | 元素必须为正数或 0       |
| @Range           | @Range(min=最小值, max=最大值)             | BigDecimal / BigInteger / CharSequence / 数字类型 | 元素必须在范围内         |
| @Size            | @Size(min=最小值, max=最大值)              | CharSequence / Collection / Map / Array       | 元素必须在长度范围内       |
| @Valid           | @Valid                               | 对象                                            | 级联验证             |

更多注解可参考包：`org.hibernate.validator`。

Cloud 版本这里的参数校验方式与 Vue 版本基本一致，可直接参考本页。
