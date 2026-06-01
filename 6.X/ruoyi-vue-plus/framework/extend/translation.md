# 翻译功能
- - -

## 模块位置

翻译功能由公共翻译模块提供：

```text
ruoyi-common/ruoyi-common-translation
```

核心类：

```text
annotation/Translation.java
annotation/TranslationType.java
core/TranslationInterface.java
core/handler/TranslationJsonFieldProcessor.java
constant/TransConstant.java
```

## 内置翻译类型

内置常量在 `TransConstant` 中定义：

| 常量 | type | 说明 |
| --- | --- | --- |
| `USER_ID_TO_NAME` | `user_id_to_name` | 用户 ID 转账号 |
| `USER_ID_TO_NICKNAME` | `user_id_to_nickname` | 用户 ID 转昵称 |
| `DEPT_ID_TO_NAME` | `dept_id_to_name` | 部门 ID 转名称 |
| `DICT_TYPE_TO_LABEL` | `dict_type_to_label` | 字典值转标签 |
| `OSS_ID_TO_URL` | `oss_id_to_url` | OSS ID 转 URL |

对应实现位于：

```text
core/impl/UserNameTranslationImpl.java
core/impl/NicknameTranslationImpl.java
core/impl/DeptNameTranslationImpl.java
core/impl/DictTypeTranslationImpl.java
core/impl/OssUrlTranslationImpl.java
```

## 使用方式

在 VO 字段上标注 `@Translation`：

```java
private Long userId;

@Translation(type = TransConstant.USER_ID_TO_NICKNAME, mapper = "userId")
private String nickName;
```

字典翻译：

```java
@Translation(type = TransConstant.DICT_TYPE_TO_LABEL, mapper = "status", other = "sys_normal_disable")
private String statusName;
```

OSS 文件地址翻译：

```java
private String ossId;

@Translation(type = TransConstant.OSS_ID_TO_URL, mapper = "ossId")
private String url;
```

## 自定义翻译

实现 `TranslationInterface` 并标注 `@TranslationType`：

```java
@TranslationType(type = "order_id_to_no")
@Component
public class OrderNoTranslationImpl implements TranslationInterface<String> {

    @Override
    public String translation(Object key, String other) {
        return orderService.getOrderNo(String.valueOf(key));
    }
}
```

使用：

```java
@Translation(type = "order_id_to_no", mapper = "orderId")
private String orderNo;
```

## 使用注意

- 翻译在 JSON 序列化阶段执行，主要用于接口返回展示。
- 大列表、导出、批量接口要谨慎使用，远程查询类翻译必须做缓存或批量处理。
- `type` 必须和 `@TranslationType` 完全一致。
- `mapper` 指向来源字段；不配置时通常使用当前字段值作为 key。
