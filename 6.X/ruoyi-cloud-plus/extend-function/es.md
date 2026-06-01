# ES 搜索引擎
- - -

## 环境搭建

如果已搭建 ELK，可跳过此步骤。  
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
docker-compose up -d elasticsearch
```

## Easy-ES 文档

- https://www.easy-es.cn/

## 用法参考

基础配置与用法参考 `ruoyi-demo` 模块，更多高级用法请参考 Easy-ES 文档。

![输入图片说明](https://foruda.gitee.com/images/1660030085169129908/屏幕截图.png "屏幕截图.png")
