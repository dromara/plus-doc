### 配置调度中心客户端
> 修改主服务配置文件
> 
![输入图片说明](https://images.gitee.com/uploads/images/2021/1027/104037_f7f702e7_1766278.png "屏幕截图.png")

* `enabled` 可启用或关闭客户端注册
* `admin-addresses` 为调度中心地址
* `access-token` 为调度中心交互鉴权token
* `executor` 为执行器配置 一个客户端为一个执行器 可配置执行器集群 使用分片任务处理

### 启用调度中心
**默认账号密码 `admin` `123456` 账号在数据库里 可以在页面修改密码**

> 在 `扩展项目 -> xxl-job-admin模块` 启动
> 
![输入图片说明](https://images.gitee.com/uploads/images/2021/1027/104404_2d29a798_1766278.png "屏幕截图.png")

> 需修改配置文件数据库连接地址(**注意: 此处为xxl-job-admin服务的配置文件**)
> 
![输入图片说明](https://images.gitee.com/uploads/images/2021/1027/104441_78319ca3_1766278.png "屏幕截图.png")

> 也可配置邮件发送
> 
![输入图片说明](https://images.gitee.com/uploads/images/2021/1027/104459_5358f30a_1766278.png "屏幕截图.png")

### 前端修改任务调度中心访问路径
`dev`环境 默认使用 `.env.development` 配置文件内地址

![输入图片说明](https://images.gitee.com/uploads/images/2021/1027/104533_e43f1e2e_1766278.png "屏幕截图.png")

`prod`环境 使用 `.env.production` 本机路由

![输入图片说明](https://images.gitee.com/uploads/images/2021/1027/104549_891a854f_1766278.png "屏幕截图.png")

故而 `prod` 环境只需更改 `nginx` 反向代理路径即可

![输入图片说明](https://images.gitee.com/uploads/images/2021/1027/104620_2247699f_1766278.png "屏幕截图.png")
