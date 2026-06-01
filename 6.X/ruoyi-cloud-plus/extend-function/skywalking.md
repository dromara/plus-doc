# SkyWalking 搭建与集成
- - -

## 服务搭建

参考文章：

- [SpringBoot 整合 SkyWalking 8.X (包含 Logback 日志采集)](https://lionli.blog.csdn.net/article/details/127656534)

框架内置 docker-compose 编排，可直接启动：

```shell
docker-compose up -d elasticsearch sky-oap sky-ui
```

## 本地开发

参考上方文章即可。

## Docker 部署

上传探针到服务器 `/docker/skywalking/agent`：

**注意：请使用框架自带探针，内含官网未提供的插件。**

![输入图片说明](https://foruda.gitee.com/images/1667453098143152651/f1b4f492_1766278.png "屏幕截图")

在服务的 `dockerfile` 中开启 SkyWalking 相关参数：

![输入图片说明](https://foruda.gitee.com/images/1667452514896786032/f4322fb9_1766278.png "屏幕截图")

在 docker-compose 中增加探针路径映射：

![输入图片说明](https://foruda.gitee.com/images/1667453276389844864/7e139aa9_1766278.png "屏幕截图")

## 日志推送（不推荐）

建议使用 ELK 统一收集日志。  
如需 SkyWalking 日志推送，请在服务中引入：

```xml
<dependency>
    <groupId>com.ruoyi</groupId>
    <artifactId>ruoyi-common-skylog</artifactId>
</dependency>
```

在 `logback.xml` 中引入 skylog 配置：

![输入图片说明](https://foruda.gitee.com/images/1667452697748002725/a18212cd_1766278.png "屏幕截图")
