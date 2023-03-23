# Only one connection receive subscriber allowed
- - -
## 问题原因
**经多人反馈 共同点为全都是做`小程序开发`使用的`uniapp`发送的网络请求而出现这种问题**

`uniapp` 错误设置 `Content-Type` 将所有请求类型全都设置成了 `json` 导致不该读body的请求也读取了body 最终导致报错

## 解决方案

方案1: 升级 1.4.0 已经对这种不合规发的请求做了兼容处理(被迫)<br>
方案2: `uniapp` 内的请求设置正确的 `Content-Type`