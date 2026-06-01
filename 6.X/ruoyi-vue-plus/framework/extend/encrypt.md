# 数据加解密
- - -

## 模块位置

数据库字段加解密由公共加密模块提供：

```text
ruoyi-common/ruoyi-common-encrypt
```

核心类：

```text
annotation/EncryptField.java
interceptor/MybatisEncryptInterceptor.java
core/EncryptorManager.java
properties/EncryptorProperties.java
```

单体项目全局配置在：

```text
ruoyi-admin/src/main/resources/application.yml
```

配置前缀：

```text
mybatis-encryptor
```

## 使用方式

在实体字段上标注 `@EncryptField`：

```java
@EncryptField
private String phone;
```

指定算法和密钥：

```java
@EncryptField(
    algorithm = AlgorithmType.RSA,
    publicKey = "公钥",
    privateKey = "私钥"
)
private String idCard;
```

支持参数：

| 参数 | 说明 |
| --- | --- |
| `algorithm` | 加密算法，未指定时使用全局配置 |
| `password` | AES、SM4 使用 |
| `publicKey` | RSA、SM2 使用 |
| `privateKey` | RSA、SM2 使用 |
| `encode` | 编码方式 |

支持算法：

```text
BASE64
AES
RSA
SM2
SM4
```

示例代码可参考：

```text
ruoyi-modules/ruoyi-demo/src/main/java/org/dromara/demo/domain/TestDemoEncrypt.java
```

## 生效流程

`mybatis-encryptor.enable=true` 时会注册 `MybatisEncryptInterceptor`：

1. MyBatis 写入前扫描实体字段上的 `@EncryptField`。
2. 对 `String` 类型字段加密。
3. 查询结果映射回实体时自动解密。

## 使用注意

- 当前只处理 `String` 字段。
- 查询、写入建议使用实体对象承载参数。
- 自定义 XML SQL 如果绕过实体字段，框架无法读取 `@EncryptField`。
- `LambdaQueryWrapper` 这类没有实体字段信息的条件，无法自动处理加密字段。
- 加密字段不适合直接做模糊查询；等值查询也需要确保查询条件按同样算法加密。
