# Only one connection receive subscriber allowed
- - -
## 问题原因

经多人反馈 共同点为全都是做` 小程序开发` 使用的 `uniapp` 发送的网络请求而出现这种问题**

## 常见原因

在小程序或 `uniapp` 场景中，错误设置了 `Content-Type`，导致不应读取请求体的请求也被当作 JSON 处理，引发异常。


## 解决方案

1. 升级到已兼容该问题的框架版本。
2. 在 `uniapp` 中为不同请求类型设置正确的 `Content-Type`。
