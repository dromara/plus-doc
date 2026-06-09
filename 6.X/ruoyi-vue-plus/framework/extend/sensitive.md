# 数据脱敏
- - -

## 模块位置

脱敏功能由公共脱敏模块提供：

```text
ruoyi-common/ruoyi-common-sensitive
```

核心类：

```text
annotation/Sensitive.java
core/SensitiveStrategy.java
core/SensitiveService.java
handler/SensitiveJsonFieldProcessor.java
```

脱敏发生在 JSON 序列化阶段，不会修改数据库原始值。

## VO 实战示例

脱敏建议直接写在返回给前端的 VO 上，不要写在数据库实体上，避免影响内部业务处理。

```java
@Data
public class CustomerVo implements Serializable {

    private Long customerId;

    private String customerName;

    @Sensitive(strategy = SensitiveStrategy.PHONE)
    private String mobile;

    @Sensitive(strategy = SensitiveStrategy.EMAIL)
    private String email;

    @Sensitive(strategy = SensitiveStrategy.ID_CARD, roleKey = {"admin"}, perms = {"crm:customer:sensitive"})
    private String idCard;

    @Sensitive(strategy = SensitiveStrategy.ADDRESS)
    private String address;
}
```

返回效果示例：

| 字段 | 原值 | 普通用户看到 | 有权限用户看到 |
| --- | --- | --- | --- |
| `mobile` | `13812345678` | `138****5678` | `13812345678` |
| `email` | `test@example.com` | `t***@example.com` | `test@example.com` |
| `idCard` | `320101199001011234` | `320***********1234` | `320101199001011234` |

如果某个页面需要“查看完整号码”按钮，建议单独提供受控接口，并在接口上做权限、日志和二次确认，不要为了单个页面取消 VO 脱敏。

## 使用方式

在返回对象字段上标注 `@Sensitive`：

```java
@Sensitive(strategy = SensitiveStrategy.PHONE)
private String phone;
```

指定可查看明文的角色或权限：

```java
@Sensitive(
    strategy = SensitiveStrategy.ID_CARD,
    roleKey = {"admin"},
    perms = {"system:user:query"}
)
private String idCard;
```

`SensitiveService.isSensitive(roleKey, perms)` 返回需要脱敏时，序列化会按策略处理字段。

## 内置策略

`SensitiveStrategy` 已内置：

```text
ID_CARD
PHONE
ADDRESS
EMAIL
BANK_CARD
CHINESE_NAME
FIXED_PHONE
USER_ID
PASSWORD
IPV4
IPV6
CAR_LICENSE
FIRST_MASK
STRING_MASK
MASK_HIGH_SECURITY
CLEAR
CLEAR_TO_NULL
```

## 自定义策略

简单规则可以直接在 `SensitiveStrategy` 中新增枚举：

```java
ORDER_NO(s -> DesensitizedUtils.mask(s, 4, 4, 6))
```

如果需要按登录用户、角色、权限决定是否脱敏，实现 `SensitiveService`：

```java
@Service
public class CustomSensitiveService implements SensitiveService {

    @Override
    public boolean isSensitive(String[] roleKey, String[] perms) {
        return !LoginHelper.isSuperAdmin();
    }
}
```

## 使用注意

- 脱敏只影响接口响应，不影响数据库值和服务内部对象值。
- 只对经过统一 JSON 序列化链路返回的数据生效。
- 导出、手动拼接 JSON、Map 转换等场景需要单独确认是否经过脱敏处理。
- 私钥、Token、证件号等高敏字段建议使用 `MASK_HIGH_SECURITY` 或 `CLEAR`。
