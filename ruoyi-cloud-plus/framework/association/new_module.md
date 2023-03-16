# 创建新服务
- - -
### 最简单的方式
> 找个配置好的 例如 `ruoyi-system` 直接copy一份

将 `pom` 名称改掉<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0228/172617_db9b6e91_1766278.png "屏幕截图.png")

服务启动类 名称改掉<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0228/172634_427aa284_1766278.png "屏幕截图.png")

`application.yml` 配置服务应用名 改掉<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0228/172656_4ff8b106_1766278.png "屏幕截图.png")

`nacos` 新建一份新的 对应新模块名称的 配置文件<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0228/172929_b7c02adb_1766278.png "屏幕截图.png")

更改 `nacos` 上的 `ruoyi-gateway.yml` 增加新服务路由<br>
新服务访问路径 `网关ip:端口/服务路径/controller路径/接口路径`<br>
例子: `http://localhost:8080/system/user/list` <br>
![输入图片说明](https://foruda.gitee.com/images/1666861595048863422/9e9755b3_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1666861629037264535/bdfd5484_1766278.png "屏幕截图")