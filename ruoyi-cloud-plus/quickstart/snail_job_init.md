# 搭建SnailJob任务调度中心(5.2.0新功能)
- - -

### 配置调度中心客户端
> 修改主服务配置文件
>

![输入图片说明](https://foruda.gitee.com/images/1687656939847353725/951c1af7_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1714355720408959262/b959f9b6_1766278.png "屏幕截图")

* `enabled` 可启用或关闭客户端注册
* `server.address` 为调度中心地址
* `server.port` 为调度中心通信端口
* `token` 为组通信校验token(可在调度中心组配置更换)
* `group-name` 为执行器组
* `namespace` 作用域(不同作用域相互隔离请勿填错)

### 启用调度中心
**需执行 easy_retry.sql 默认账号密码 `admin` `admin` 账号在数据库里 可以在页面修改密码**
<br>

![输入图片说明](https://foruda.gitee.com/images/1714355875395308961/adc21668_1766278.png "屏幕截图")

> 在 `ruoyi-extend -> ruoyi-easyretry-server` 模块启动
>
![输入图片说明](https://foruda.gitee.com/images/1714355975617591987/ec9c0a41_1766278.png "屏幕截图")

> 需修改配置文件数据库连接地址(**注意: 此处为ruoyi-easyretry-server服务的配置文件 支持多种不同数据库**)
>
![输入图片说明](https://foruda.gitee.com/images/1714356048711590477/13289085_1766278.png "屏幕截图")

### 前端修改任务调度中心访问路径
`dev`环境 默认使用 `.env.development` 配置文件内地址

![输入图片说明](https://foruda.gitee.com/images/1714356140349263410/00a21ede_1766278.png "屏幕截图")

`prod`环境 使用 `.env.production` 本机路由

![输入图片说明](https://foruda.gitee.com/images/1714356165432505626/d4e84659_1766278.png "屏幕截图")

故而 `prod` 环境只需更改 `nginx` 反向代理路径即可

![输入图片说明](https://foruda.gitee.com/images/1714356206209822265/4796536f_1766278.png "屏幕截图")