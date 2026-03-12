# 短信模块
- - -

## 版本与配置

### 版本 >= 2.1.0（sms4j）

已完成 sms4j 集成，文档地址：https://sms4j.com/doc3/

配置方式与厂商扩展请参考 sms4j 文档。

![输入图片说明](https://foruda.gitee.com/images/1705573035997239848/2ca8512d_1766278.png "屏幕截图")

使用方式可参考 demo 模块示例：

![输入图片说明](https://foruda.gitee.com/images/1705573001447394180/2bd726d0_1766278.png "屏幕截图")

### 版本 1.2.0（SPI 方式）

短信模块采用 SPI 加载，支持 `阿里云`、`腾讯云`，可提交 PR 扩展。

参考 `ruoyi-demo` 的 pom 配置：

![输入图片说明](https://foruda.gitee.com/images/1678979157797419426/cc9b7444_1766278.png "屏幕截图")

配置文件示例：

![输入图片说明](https://foruda.gitee.com/images/1678979163029635375/e5fd6e20_1766278.png "屏幕截图")

参数说明：

- `enabled`：短信功能开关
- `endpoint`：厂家域名
- `accessKeyId`：密钥 ID
- `accessKeySecret`：密钥
- `signName`：签名
- `sdkAppId`：应用 ID（腾讯专用）

## 功能使用

参考 demo 模块 `SmsController` 示例。  
功能采用“模板模式”动态加载厂商模板，注入 `SmsTemplate` 即可使用。

![输入图片说明](https://foruda.gitee.com/images/1678979168699323982/e9301e84_1766278.png "屏幕截图")

## 重点须知

不同厂家参数格式差异较大，请按规则配置：

![输入图片说明](https://foruda.gitee.com/images/1678979172581090456/ac1f10e8_1766278.png "屏幕截图")
