# (旧)应用部署
- - -
## 手动部署

在服务器安装 `nacos(对接mysql)` `mysql` `redis` `nginx` `minio` 等其他组件

将项目内 `docker/` 文件夹下的文件内容 放到对应的组件内<br>
例如: 将项目内 `docker/nginx/nginx.conf` 配置文件 复制到 `nginx` 配置内<br>
将项目内 `docker/redis/redis.conf` 配置文件 复制到 `redis` 配置内<br>
将项目内 `docker/nacos/custom.properties` 配置文件 复制到 `nacos` 配置内<br>

并修改相关参数如 `前端页面存放位置` `后端Ip地址` 等使其生效

jar包部署后端服务 打包命令如下
```mvn
mvn clean install -D maven.test.skip=true -P prod
```
## docker 后端部署

> [docker安装](https://lionli.blog.csdn.net/article/details/83153029)<br>
> [docker-compose安装](https://lionli.blog.csdn.net/article/details/111220320)<br>
> [docker网络模式讲解](https://lionli.blog.csdn.net/article/details/109603785)<br>
> [docker 开启端口 2375 供外部程序访问](https://lionli.blog.csdn.net/article/details/92627962)

### 将源码内 `docker` 文件夹上传到服务器(注意: 不要放到根目录)

进入 `docker` 目录 给shell脚本分配执行权限
```shell
chmod 777 ~/docker/deploy.sh
```

### 开放外网防火墙端口(内网服务无需开启)
```shell
sh deploy.sh port
```

### 放置挂载文件(切勿多次执行)
```shell
sh deploy.sh mount
```

### 分配文件夹权限
**重点注意: 一定要确保目录 `/docker` 及其所有子目录 具有写权限 如果后续出现权限异常问题 重新执行一遍分配权限**
```shell
chmod -R 777 /docker
```

### 启动基础服务
```shell
sh deploy.sh base
```
### 启动可视化服务
```shell
sh deploy.sh monitor
```

### 启动与停止业务服务(需要先构建服务镜像)
```shell
sh deploy.sh start
sh deploy.sh stop
```

### 停止所有服务
```shell
sh deploy.sh stopall
```

### 删除所有容器
```shell
sh deploy.sh rm
```

### 删除所有空版本镜像
```shell
sh deploy.sh rmiNoneTag
```

### 构建服务镜像

首先 使用 `maven` 总工程打包 所有模块jar包(注意: 此处需使用`install`因有几个依赖工程需要装载到本地)

![输入图片说明](https://images.gitee.com/uploads/images/2022/0802/143055_0c6bf29e_1766278.png "屏幕截图.png")

然后 使用 `docker-maven-plugin` 插件上传构建 `ruoyi-server` 镜像

需修改 `pom` 文件对应 `docker` 服务器的 `ip` 地址<br>
与 `docker` 服务配置开启 `2375` api端口 [docker 开启端口 2375 供外部程序访问](https://lionli.blog.csdn.net/article/details/92627962)

> 未开启 `2375` api端口将无法远程连接 `docker`<br>
> 可选使用 ssh 上传 jar 包 在服务器执行 `docker build` 构建镜像 命令具体用法参考文章: [docker build 方式部署jar包](https://blog.csdn.net/qq_31360283/article/details/126487908)

![输入图片说明](https://images.gitee.com/uploads/images/2021/0727/115512_1f043312_1766278.png "屏幕截图.png")

对应maven命令(对应模块目录内执行)
```shell
cd ruoyi-admin
mvn docker:build
```


## 前端部署

执行打包命令
```shell
# 打包正式环境
npm run build:prod
```
打包后生成打包文件在 `ruoyi-ui/dist` 目录<br>
将 `dist` 目录下文件(不包含 `dist` 目录) 上传到部署服务器 `docker/nginx/html` 目录下(手动部署放入自己配置的路径即可)<br>
重启 `nginx` 服务即可

