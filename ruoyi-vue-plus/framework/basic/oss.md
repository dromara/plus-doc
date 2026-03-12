# 关于 OSS 模块使用
- - -

## 重点注意事项

- 访问站点不要携带路径（如 `/`、`/ruoyi`）
- 阿里云与腾讯云：访问站点中不要包含桶名，系统会自动处理
- MinIO：站点不建议使用 `localhost`，请使用 `127.0.0.1`
- 访问站点与自定义域名不要包含 `http/https` 前缀，HTTPS 请使用配置项控制
- 4.4.0 版本支持配置公有/私有权限（阿里云需开启跨域配置）

## 代码使用

参考 `SysOssService.upload` 的用法。  
使用 `OssFactory.instance()` 获取当前启用的 `OssClient` 实例，执行上传并保存返回结果到业务表。

![输入图片说明](https://foruda.gitee.com/images/1678978345529639839/d350ec0b_1766278.png "屏幕截图")

## 功能配置

### 1. 配置 OSS

进入 `系统管理 -> 文件管理 -> 配置管理` 填写 OSS 配置。

![输入图片说明](https://foruda.gitee.com/images/1678978349820700551/1f91a237_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1678978354387669856/3a91a3a9_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1678978358019307086/0c2523e4_1766278.png "屏幕截图")

重点说明：云厂商只需修改 `访问站点` 对应域名，尽量不要修改其他参数。  
云厂商建议绑定自定义域名使用（七牛云为强制要求）。

![输入图片说明](https://foruda.gitee.com/images/1678978362358100362/5c2c4d20_1766278.png "屏幕截图")

示例：

- 七牛云访问站点

![输入图片说明](https://foruda.gitee.com/images/1678978366254745764/e93a65ff_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1678978369853348732/79e8950e_1766278.png "屏幕截图")

- 阿里云访问站点

![输入图片说明](https://foruda.gitee.com/images/1678978373981462025/56a70398_1766278.png "屏幕截图")

- 腾讯云访问站点

![输入图片说明](https://foruda.gitee.com/images/1678978378697093134/785517f3_1766278.png "屏幕截图")

### 2. MinIO 使用 HTTPS 访问

**注意：S3 API 签名算法不支持托管 MinIO Server API 的代理方案。**

[minio https 配置方式](https://blog.csdn.net/Michelle_Zhong/article/details/126484358)

### 3. 切换 OSS 配置

在配置列表中点击 `状态` 启用即可（一次仅能启用一个默认配置）。  
也可使用 `OssFactory.instance("configKey")` 指定配置。

![输入图片说明](https://foruda.gitee.com/images/1678978383700118702/7f3fa0c5_1766278.png "屏幕截图")

### 4. 扩展分类

如需文件分类，建议创建多个 OSS 配置进行切换存储：

- 通过不同 `configKey` / 前缀目录区分
- 或使用独立桶（可分别设置访问权限）

![输入图片说明](https://foruda.gitee.com/images/1678978389139754119/140be1df_1766278.png "屏幕截图")

指定配置示例：

```java
OssClient client = OssFactory.instance("image");
```

![输入图片说明](https://foruda.gitee.com/images/1678978397550123641/1b536881_1766278.png "屏幕截图")

## 功能使用

### 上传文件或图片

在 `系统管理 -> 文件管理` 中点击 `上传文件` 或 `上传图片`。

![输入图片说明](https://foruda.gitee.com/images/1678978401028132972/445d058e_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1678978404388284503/5459da29_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1678978408761764835/c81651fc_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1678978412748494539/7bae621f_1766278.png "屏幕截图")

### 列表展示与预览

默认展示图片（可预览），文件显示路径。

![输入图片说明](https://foruda.gitee.com/images/1678978416327601385/af1ecb3b_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1678978422249633007/19d68eaa_1766278.png "屏幕截图")

可通过 `预览禁用/启用` 切换展示方式：

![输入图片说明](https://foruda.gitee.com/images/1678978426017014926/4f7fa3f3_1766278.png "屏幕截图")

禁用后图片会显示为路径：

![输入图片说明](https://foruda.gitee.com/images/1678978429692592556/0231d778_1766278.png "屏幕截图")

也可在 `参数设置` 中将 `OSS预览列表资源` 设为 `false` 统一关闭预览：

![输入图片说明](https://foruda.gitee.com/images/1678978433769403801/7d480e76_1766278.png "屏幕截图")

### 删除与下载

删除会根据 OSS 服务商类型调用对应删除接口。  
可勾选多服务商类型文件进行批量删除。

![输入图片说明](https://foruda.gitee.com/images/1678978438265941745/f32edc72_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678978441938542080/43ed7c3d_1766278.png "屏幕截图")

下载可填写文件名并确认：

![输入图片说明](https://foruda.gitee.com/images/1678978448927336261/409af888_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678978452761792483/ed0a4a72_1766278.png "屏幕截图")
