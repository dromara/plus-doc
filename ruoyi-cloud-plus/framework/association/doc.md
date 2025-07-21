# 接口文档
- - -
## 版本 >= `1.2.0`
## 说明
由于 `springfox` 与 `knife4j` 均停止维护 bug众多<br>
故从 `1.2.0` 开始 迁移到 `springdoc` 框架<br>
基于 `javadoc` 无注解零入侵生成规范的 `openapi` 结构体<br>
由于框架自带文档UI功能单一扩展性差 故移除自带UI 建议使用外置文档工具

## 文档工具使用
由于框架采用 `openapi` 行业规范 故市面上大部分的框架均支持 可自行选择<br>
例如: `apifox` `apipost` `postman` `torna` `knife4j` 等 根据对应工具的文档接入即可

## Swagger升级SpringDoc指南

常见功能如下 其他功能自行挖掘<br>
**注意: `javadoc` 只能替换基础功能 特殊功能还需要使用注解实现**

| swagger                          | springdoc                       | javadoc            |
|----------------------------------|---------------------------------|--------------------|
| @Api(name = "xxx")               | @Tag(name = "xxx")              | java类注释第一行         |
| @Api(description= "xxx")         | @Tag(description= "xxx")        | java类注释            |
| @ApiOperation                    | @Operation                      | java方法注释           | 
| @ApiIgnore                       | @Hidden                         | 无                  | 
| @ApiParam                        | @Parameter                      | java方法@param参数注释   | 
| @ApiImplicitParam                | @Parameter                      | java方法@param参数注释   | 
| @ApiImplicitParams               | @Parameters                     | 多个@param参数注释       | 
| @ApiModel                        | @Schema                         | java实体类注释          | 
| @ApiModelProperty                | @Schema                         | java属性注释           | 
| @ApiModelProperty(hidden = true) | @Schema(accessMode = READ_ONLY) | 无                  | 
| @ApiResponse                     | @ApiResponse                    | java方法@return返回值注释 | 

## 建议使用 `Apifox`(常见问题有其他对接方式)

官网连接: [https://www.apifox.cn/](https://www.apifox.cn/)<br>
视频教程: [springdoc与apifox配合使用](https://www.bilibili.com/video/BV1mr4y1j75M?p=8&vd_source=8f52c77be3233dbdd1c5e332d4d45bfb)

![输入图片说明](https://foruda.gitee.com/images/1678976476639902970/f1617b40_1766278.png "屏幕截图")

支持 文档编写 接口调试 Mock 接口压测 自动化测试 等一系列功能

### 使用 OpenApi 接入框架

#### 1：创建项目
> 下载或使用web在线版 创建一个自己的项目<br>

![输入图片说明](https://foruda.gitee.com/images/1678976502850663851/7bbd8728_1766278.png "屏幕截图")

#### 2：导入项目设置
> 进入项目 选择项目设置 找到自动同步<br>

![输入图片说明](https://foruda.gitee.com/images/1678976508918240326/6a4a61a8_1766278.png "屏幕截图")

#### 3：数据源创建
> 根据项目内所有文档组完成所有数据源创建(拉取后端`openapi`结构体)<br>
数据源URL格式 `http://网关ip:端口/服务路径/v3/api-docs`<br>
项目内所需:<br>
`http://localhost:8080/demo/v3/api-docs` 演示服务<br>
`http://localhost:8080/auth/v3/api-docs` 认证服务<br>
`http://localhost:8080/resource/v3/api-docs` 资源服务<br>
`http://localhost:8080/system/v3/api-docs` 系统服务<br>
`http://localhost:8080/code/v3/api-docs` 代码生成服务<br>

![输入图片说明](https://foruda.gitee.com/images/1678980352012289965/24e0e4da_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1678980368645148754/62308680_1766278.png "屏幕截图")

#### 4：自动导入
> 选择 接口管理 项目概览 点击立即导入 并等待导入完成<br>
后续会根据策略每3个小时自动导入一次<br>
每次重新进入apifox也会自动同步一次<br>
后端有改动也可以手动点击导入<br>

![输入图片说明](https://foruda.gitee.com/images/1678980393851604773/a0c657d3_1766278.png "屏幕截图")

#### 5：鉴权设置（注意版本号）
> 设置鉴权 选择接口管理 项目概览 找到Auth 按照如下配置<br>

**版本号: >= 2.X**

![输入图片说明](https://foruda.gitee.com/images/1690966897370710566/6a688aea_1766278.png "屏幕截图")

**版本号: 1.X**

![输入图片说明](https://foruda.gitee.com/images/1678980398409729963/db4502a0_1766278.png "屏幕截图")

> key对应项目配置 默认为 `Authorization`<br>

![输入图片说明](https://foruda.gitee.com/images/1678976544342001474/c2ff85d3_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1678976549237304743/bcdfadda_1766278.png "屏幕截图")

### 使用 Apifox-Helper 接入框架

官方文档：[Apifox官方文档 - IDEA 插件](https://docs.apifox.com/doc-5743620)

创建一个 ApiKey 用于上传接口文档：

![输入图片说明](https://foruda.gitee.com/images/1753102590437056663/6a9604f0_4959041.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1753102633891623034/69428c34_4959041.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1753102720063363982/16c95783_4959041.png "屏幕截图")

#### 1：插件安装

> IDEA 插件安装：目前最新版本 **v2.0.13-243**
 
![输入图片说明](https://foruda.gitee.com/images/1753100791977471774/ac854016_4959041.png "屏幕截图")

#### 2：界面展示

打开项目时显示：

![输入图片说明](https://foruda.gitee.com/images/1753100862453931298/0d887f2a_4959041.png "屏幕截图")

可以手动点击刷新：

![输入图片说明](https://foruda.gitee.com/images/1753100872505206360/109c6242_4959041.png "屏幕截图")

如果觉得地方不够可以使用悬浮窗：

![输入图片说明](https://foruda.gitee.com/images/1753101862045577580/85983315_4959041.png "屏幕截图")

悬浮窗，拉到合适大小：

![输入图片说明](https://foruda.gitee.com/images/1753101929442545957/34b252c1_4959041.png "屏幕截图")

可以切换分屏位置：

![输入图片说明](https://foruda.gitee.com/images/1753101038593037694/5a25975e_4959041.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1753101949858940541/d16e3e6d_4959041.png "屏幕截图")

在插件中使用方式与web版本、客户端版本基本一致，如果只是简单进行测试可以直接使用，在此不再赘述。

下面重点说明使用插件进行 Apidoc 上传。

#### 3：将 Apidoc 上传到 Apifox

前面介绍的使用手动上传方式，需要在 `application.yml` 以及 Apifox 中分别进行相关配置。使用插件可以直接扫描出相关的模块以及模型，只需要按照标准使用相关的注解即可。

##### 3.1：新建模块

之前的用法是把所有的接口导入到默认模块中，按照文件夹来进行区分。<br/>
插件上传的时候需要选择模块，如果不单独设置，不会像原有那样可以选择文件夹。<br/>
因此这里将各模块单独独立出来，效果如下：<br/>

![输入图片说明](https://foruda.gitee.com/images/1753101309563059086/5c7de82c_4959041.png "屏幕截图")

新建模块：

![输入图片说明](https://foruda.gitee.com/images/1753101377513565932/7eb21bd1_4959041.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1753101387804054220/74421028_4959041.png "屏幕截图")

##### 3.2：上传到 Apifox

![输入图片说明](https://foruda.gitee.com/images/1753102049972873779/9ffb73cf_4959041.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1753101460286937773/c718468e_4959041.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1753102310528079364/80c0af60_4959041.png "屏幕截图")


##### 3.3：查看控制台输出

![输入图片说明](https://foruda.gitee.com/images/1753102387726090214/16aae4ab_4959041.png "屏幕截图")

##### 3.4：查看文档

![输入图片说明](https://foruda.gitee.com/images/1753102411755563077/354c132e_4959041.png "屏幕截图")

#### 4：插件配置

![输入图片说明](https://foruda.gitee.com/images/1753103060226305728/06889b21_4959041.png "屏幕截图")

更多使用方法请参考 [Apifox 官方文档](https://docs.apifox.com/doc-5743620)。