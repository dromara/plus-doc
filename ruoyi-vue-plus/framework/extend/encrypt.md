# 数据加解密
- - -

## 版本

- >= 4.6.0

## 功能说明

数据库字段在写入时加密、读取时解密。  
支持算法：`BASE64`、`AES`、`RSA`、`SM2`、`SM4`。

补充说明：

- 当前项目默认配置位于 `application.yml` 的 `mybatis-encryptor` 节点，默认是关闭状态。
- 框架通过 MyBatis 拦截器在入库和出库时自动处理加解密。

## 注解 `@EncryptField`

![输入图片说明](https://foruda.gitee.com/images/1675577493013639395/cd920f15_1766278.png "屏幕截图")

补充说明：

- `@EncryptField` 可配置 `algorithm`、`password`、`publicKey`、`privateKey`、`encode`。
- 当前实现只会处理 `String` 类型字段，其他类型不会按字段加密规则自动处理。

## 使用方式

详细用法可参考 `TestEncryptController` 示例。

### 1. 全局默认配置

注解未指定时使用全局配置。

![输入图片说明](https://foruda.gitee.com/images/1675577674063566357/dee94786_1766278.png "屏幕截图")

### 2. 注解自定义配置

可在注解中指定算法与密钥配置。

![输入图片说明](https://foruda.gitee.com/images/1675577725117970708/7ee7a833_1766278.png "屏幕截图")

## 密钥生成说明

![输入图片说明](https://foruda.gitee.com/images/1675577852271308699/9b30258e_1766278.png "屏幕截图")

## 注意事项

- 必须使用实体类参与查询与持久化
- 自定义 XML SQL 也应传入实体类
- `LambdaQueryWrapper` 等无实体信息的查询无法获取加密注解，可能导致加密失效

补充说明：

- 如果自定义 SQL 查询结果不再映射回带有 `@EncryptField` 的实体类，也无法自动解密。
- 因此字段加密场景下，建议优先保持“实体类入参 + 实体类出参”的使用方式。
