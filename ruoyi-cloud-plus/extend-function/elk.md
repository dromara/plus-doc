# ELK 搭建
- - -

## 环境搭建

项目内置 ELK 的 docker-compose 编排，位于 `/docker/docker-compose.yml` 的扩展部分。

**注意：`/docker/elk/elasticsearch/` 目录下所有文件夹需写权限。**

```shell
chmod 777 /docker/elk/elasticsearch/data
chmod 777 /docker/elk/elasticsearch/logs
chmod 777 /docker/elk/elasticsearch/plugins
```

**ES 插件需解压后放入 `plugins` 目录。**

## 启动命令

```shell
docker-compose up -d elasticsearch kibana logstash
```

## 参考文章

- [docker-compose 搭建 ELK 7.X 并整合 SpringBoot](https://lionli.blog.csdn.net/article/details/125743132)

## 项目内配置

服务引入依赖：

```xml
<dependency>
    <groupId>com.ruoyi</groupId>
    <artifactId>ruoyi-common-logstash</artifactId>
</dependency>
```

修改主 `pom` 中 `logstash.address`：

![输入图片说明](https://foruda.gitee.com/images/1678981534923588112/ba6cb5b7_1766278.png "屏幕截图")
