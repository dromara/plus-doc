# 创建新服务
- - -

## 快速方式

复制已有服务（如 `ruoyi-system`）作为模板。

## 必要改动

1. 修改 `pom` 名称

![输入图片说明](https://foruda.gitee.com/images/1678980168782983123/c717e9ba_1766278.png "屏幕截图")

2. 修改启动类名称

![输入图片说明](https://foruda.gitee.com/images/1678980179829877203/f89d5c18_1766278.png "屏幕截图")

3. 修改 `application.yml` 服务名

![输入图片说明](https://foruda.gitee.com/images/1678980184047648028/e4c6c6cc_1766278.png "屏幕截图")

4. 在 Nacos 新增对应服务配置

![输入图片说明](https://foruda.gitee.com/images/1678980188806372269/cfd9731a_1766278.png "屏幕截图")

5. 在 `ruoyi-gateway.yml` 增加路由

新服务访问路径：

`网关ip:端口/服务路径/controller路径/接口路径`

示例：`http://localhost:8080/system/user/list`

![输入图片说明](https://foruda.gitee.com/images/1666861595048863422/9e9755b3_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1666861629037264535/bdfd5484_1766278.png "屏幕截图")

## 注意事项

- 不同包名的模块需同步修改配置

![输入图片说明](https://foruda.gitee.com/images/1719813861680271619/82435586_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1692006501957936219/059f8526_1766278.png "屏幕截图")

- 如需使用 `Seata` 分布式事务，请在 `seata-server.properties` 中增加服务组

![输入图片说明](https://foruda.gitee.com/images/1692006825427360840/5b9e410c_1766278.png "屏幕截图")
