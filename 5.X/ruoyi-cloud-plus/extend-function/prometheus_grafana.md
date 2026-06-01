# Prometheus + Grafana 搭建
- - -

## 基础搭建

参考文章：

- https://lionli.blog.csdn.net/article/details/127959009

## 框架内扩展

框架已包含 docker-compose 编排，可直接启动：

```shell
docker-compose up -d prometheus grafana
```

## 应用配置

### 1. 引入依赖

各服务引入 `ruoyi-common-prometheus`：

![输入图片说明](https://foruda.gitee.com/images/1668998415863943539/413dc560_1766278.png "屏幕截图")

### 2. 修改 Prometheus 采集配置

![输入图片说明](https://foruda.gitee.com/images/1668998433756761442/bf31c212_1766278.png "屏幕截图")

### 3. 修改 Nacos 与 Admin 地址

如均为本地应用可不修改。

![输入图片说明](https://foruda.gitee.com/images/1668998317973042740/2d3590ec_1766278.png "屏幕截图")

## 导入框架模板

**注意：数据源名称需与模板保持一致，否则无法匹配。**

![输入图片说明](https://foruda.gitee.com/images/1669866309495145064/1de987ce_1766278.png "屏幕截图")

在 Grafana 上传框架内置模板 JSON 文件：

![输入图片说明](https://foruda.gitee.com/images/1668998149634542527/f0881c8e_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1668998179391197847/b1d3a630_1766278.png "屏幕截图")

## 查看监控

在右侧菜单选择想要查看的监控项：

![输入图片说明](https://foruda.gitee.com/images/1668998515814170229/817ac8b0_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1668998567335384306/acdf2833_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1668998616894681785/ac27538b_1766278.png "屏幕截图")
