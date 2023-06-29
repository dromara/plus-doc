# Sharding-Proxy搭建分库分表
- - -
## 服务搭建

参考部署文档上传 docker 文件夹 内部包含 shardingproxy 配置文件

![输入图片说明](https://foruda.gitee.com/images/1688013921062151295/89652dda_1766278.png "屏幕截图")

框架已经包含了 docker-compose 编排 执行如下命令启动容器即可

```shell
docker-compose up -d shardingproxy
```

### 如何使用

查看 `ruoyi-demo` 服务 `TestShardingController`

![输入图片说明](https://foruda.gitee.com/images/1688014028842337522/cd26026a_1766278.png "屏幕截图")

用法参考文章: https://blog.csdn.net/zhaozhiqiang1981/article/details/129935075
用法参考视频: https://www.bilibili.com/video/BV1XN411A7Tv/
