# 配置功能

版本: v4.2.0 提供短信模块

短信模块采用SPI加载<br>
使用哪家的短信 引入哪家的依赖 即可动态加载<br>
目前支持: `阿里云` `腾讯云` 欢迎扩展PR其他

参考 `ruoyi-demo` pom文件写法
![输入图片说明](https://images.gitee.com/uploads/images/2022/0507/101022_82b165d9_1766278.png "屏幕截图.png")

修改配置文件

![输入图片说明](https://images.gitee.com/uploads/images/2022/0507/101743_961048d6_1766278.png "屏幕截图.png")

* `enabled` 为短信功能开关
* `endpoint` 为域名 各厂家域名固定 按照文档配置即可
* `accessKeyId` 密钥id
* `accessKeySecret` 密钥密匙
* `signName` 签名
* `sdkAppId` 应用id 腾讯专用

# 功能使用

参考 `demo` 模块 `SmsController` 短信演示案例<br>
功能采用 `模板模式` 动态加载对应厂家的工具模板<br>
引入 `SmsTemplate` 即可使用

![输入图片说明](https://images.gitee.com/uploads/images/2022/0507/101513_955e78c1_1766278.png "屏幕截图.png")

# 重点须知

由于各厂家参数解析不一致 请遵守以下规则

![输入图片说明](https://images.gitee.com/uploads/images/2022/0507/101648_35f4723a_1766278.png "屏幕截图.png")