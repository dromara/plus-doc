# 数据加解密
- - -

## 版本

- >= 4.6.0

## 功能说明

数据库字段在写入时加密、读取时解密。  
支持算法：`BASE64`、`AES`、`RSA`、`SM2`、`SM4`。

## 注解 `@EncryptField`

![输入图片说明](https://foruda.gitee.com/images/1675577493013639395/cd920f15_1766278.png "屏幕截图")

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
