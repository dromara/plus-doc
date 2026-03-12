# 应用部署
- - -

## 版本要求

适用于 `>= 4.3.0`。

## 前置阅读

请优先阅读 [IntelliJ IDEA 环境配置](/ruoyi-vue-plus/quickstart/idea_environment.md)。

## 部署方式选择

- 手动部署：适合已有基础设施的服务器
- Docker 部署：适合快速搭建与统一运维

## 手动部署

### 1. 安装基础服务

安装 `MySQL`、`Redis`、`Nginx`、`MinIO`。

### 2. 准备配置文件

将项目内配置复制到服务目录并按需修改：

- `script/docker/nginx/nginx.conf`
- `script/docker/redis/redis.conf`

重点修改：前端静态文件路径、后端服务地址等。

### 3. 打包后端

```mvn
mvn clean package -D maven.test.skip=true -P prod
```

### 4. 创建临时文件目录

服务端需要创建临时文件存储目录，路径需与配置文件一致。  
否则可能出现上传失败等问题。

![输入图片说明](https://foruda.gitee.com/images/1659951373949149804/屏幕截图.png "屏幕截图.png")

### 5. 启动后端服务

按实际部署方式启动生成的 `jar` 文件。

## 部署视频

[RuoYi-Vue-Plus 5.0 生产环境搭建部署](https://www.bilibili.com/video/BV1mL411e7ha/)

## Docker 后端部署

### 1. 安装 Docker 与 Compose

请优先阅读 [idea环境配置](https://gitee.com/dromara/RuoYi-Cloud-Plus/wikis/pages?sort_id=5985190&doc_id=2056143)

- [docker安装](https://lionli.blog.csdn.net/article/details/83153029)
- [docker-compose安装](https://lionli.blog.csdn.net/article/details/111220320)
- [docker网络模式讲解](https://lionli.blog.csdn.net/article/details/109603785)
- [docker 开启端口 2375 供外部程序访问](https://lionli.blog.csdn.net/article/details/92627962)

### 2. 上传配置到服务器

推荐使用 IDEA 的远程上传功能，将配置文件上传到服务器根目录。

![输入图片说明](https://foruda.gitee.com/images/1662109450908169859/eaac9299_1766278.png "屏幕截图")

### 3. 配置目录权限

确保 `/docker` 及其子目录具有写权限。  
权限不足会导致容器读写异常。

```shell
chmod -R 777 /docker
```

![输入图片说明](https://foruda.gitee.com/images/1662109847279259882/3a2202c1_1766278.png "屏幕截图")

### 4. 构建应用镜像

先使用 Maven 打包生成 `jar`，再执行镜像构建。

![输入图片说明](https://foruda.gitee.com/images/1662110477410977621/c6931c42_1766278.png "屏幕截图")

项目初始化后会自动生成构建镜像的运行配置，连接 Docker 后直接运行即可。  
**注意：IDEA 2024 及以上版本要求本地安装 Docker。**

![输入图片说明](https://foruda.gitee.com/images/1662110192257483752/0f754b47_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1662120004773449909/9fdef59c_1766278.png "屏幕截图")

结构讲解 右键编辑 即可看到内部配置

![输入图片说明](https://foruda.gitee.com/images/1662458355500139498/eaa26036_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1662458446794722159/32c086a7_1766278.png "屏幕截图")

### 5. 启动基础服务

```shell
docker-compose up -d mysql nginx-web redis minio
```

### 6. 启动业务服务

4.X：
```shell
docker-compose up -d ruoyi-monitor-admin ruoyi-xxl-job-admin ruoyi-server1 ruoyi-server2
```

5.X：
```shell
docker-compose up -d ruoyi-monitor-admin ruoyi-snailjob-server ruoyi-server1 ruoyi-server2
```

### 7. Docker 常用操作

![输入图片说明](https://foruda.gitee.com/images/1662458271941863770/cd180a04_1766278.png "屏幕截图")

## 前端部署

### 1. 构建前端

```shell
npm run build:prod
```

### 2. 上传静态资源

构建后产物位于 `ruoyi-ui/dist`。  
将 `dist` 目录内文件（不含 `dist` 本身）上传到 `docker/nginx/html`（或手动部署的静态目录）。

![输入图片说明](https://foruda.gitee.com/images/1662110914769648699/07f344c4_1766278.png "屏幕截图")

### 3. 重启 Nginx

配置更新后重启 `Nginx` 使配置生效。

## 修改代理路径或后端地址

如需变更后端代理路径或后端地址，请同时修改以下配置：

- `nginx.conf` 中的代理路径（注意 `/` 开头与结尾）
- 前端 `.env.*` 文件内的 `VITE_APP_BASE_API`
- `nginx.conf` 中的后端 IP 地址

![输入图片说明](https://foruda.gitee.com/images/1660185698211067202/屏幕截图.png "屏幕截图.png")
![输入图片说明](https://foruda.gitee.com/images/1724318035232137124/5d035a09_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1660185711265558730/屏幕截图.png "屏幕截图.png")
