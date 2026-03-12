# 接口文档
- - -

## 版本说明

- >= 1.2.0

## 背景说明

`springfox` 与 `knife4j` 已停止维护，Bug 较多。  
从 `1.2.0` 开始迁移到 `springdoc`，基于 `javadoc` 无注解生成 OpenAPI 结构。  
框架移除内置 UI，推荐使用外置文档工具。

## 文档工具选择

框架输出标准 OpenAPI，可选工具：

- `Apifox`
- `Apipost`
- `Postman`
- `Torna`
- `Knife4j`

## Swagger -> SpringDoc 映射

**注意：`javadoc` 只能替代基础功能，复杂场景仍需注解。**

| swagger                          | springdoc                       | javadoc       |
|----------------------------------|---------------------------------|---------------|
| @Api(name = "xxx")               | @Tag(name = "xxx")              | 类注释第一行        |
| @Api(description= "xxx")         | @Tag(description= "xxx")        | 类注释           |
| @ApiOperation                    | @Operation                      | 方法注释          |
| @ApiIgnore                       | @Hidden                         | 无             |
| @ApiParam                        | @Parameter                      | 方法 @param 注释  |
| @ApiImplicitParam                | @Parameter                      | 方法 @param 注释  |
| @ApiImplicitParams               | @Parameters                     | 多个 @param 注释  |
| @ApiModel                        | @Schema                         | 实体类注释         |
| @ApiModelProperty                | @Schema                         | 字段注释          |
| @ApiModelProperty(hidden = true) | @Schema(accessMode = READ_ONLY) | 无             |
| @ApiResponse                     | @ApiResponse                    | 方法 @return 注释 |

## 建议使用 `Apifox`(常见问题有其他对接方式)

官网：https://www.apifox.cn/

视频教程：https://www.bilibili.com/video/BV1mr4y1j75M?p=8

![输入图片说明](https://foruda.gitee.com/images/1678976476639902970/f1617b40_1766278.png "屏幕截图")

支持文档编写、接口调试、Mock、压测与自动化测试。

## 使用 OpenAPI 接入（Apifox）

### 1. 创建项目

下载客户端或使用 Web 版创建项目。

![输入图片说明](https://foruda.gitee.com/images/1678976502850663851/7bbd8728_1766278.png "屏幕截图")

### 2. 开启自动同步

进入项目设置，找到自动同步。

![输入图片说明](https://foruda.gitee.com/images/1678976508918240326/6a4a61a8_1766278.png "屏幕截图")

### 3. 创建数据源

根据项目服务创建数据源（拉取 `/v3/api-docs`）<br>
数据源URL格式 `http://网关ip:端口/服务路径/v3/api-docs`<br>
项目内所需:<br>

示例：

- `http://localhost:8080/demo/v3/api-docs` 演示服务<br>
- `http://localhost:8080/auth/v3/api-docs` 认证服务<br>
- `http://localhost:8080/resource/v3/api-docs` 资源服务<br>
- `http://localhost:8080/system/v3/api-docs` 系统服务<br>
- `http://localhost:8080/code/v3/api-docs` 代码生成服务<br>

![输入图片说明](https://foruda.gitee.com/images/1678980352012289965/24e0e4da_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1678980368645148754/62308680_1766278.png "屏幕截图")

### 4. 导入接口

在“接口管理 -> 项目概览”点击“立即导入”。  
后续可按策略自动同步，也可手动导入。

![输入图片说明](https://foruda.gitee.com/images/1678980393851604773/a0c657d3_1766278.png "屏幕截图")

### 5. 鉴权设置（注意版本）

**>= 2.X**

![输入图片说明](https://foruda.gitee.com/images/1690966897370710566/6a688aea_1766278.png "屏幕截图")

**1.X**

![输入图片说明](https://foruda.gitee.com/images/1678980398409729963/db4502a0_1766278.png "屏幕截图")

默认 key 为 `Authorization`：

![输入图片说明](https://foruda.gitee.com/images/1678976544342001474/c2ff85d3_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678976549237304743/bcdfadda_1766278.png "屏幕截图")

## 使用 Apifox-Helper

官方文档：https://docs.apifox.com/doc-5743620

### 1. 创建 ApiKey

![输入图片说明](https://foruda.gitee.com/images/1753102590437056663/6a9604f0_4959041.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1753102633891623034/69428c34_4959041.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1753102720063363982/16c95783_4959041.png "屏幕截图")

### 2. 插件安装

![输入图片说明](https://foruda.gitee.com/images/1753100791977471774/ac854016_4959041.png "屏幕截图")

### 3. 插件界面

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

### 4. 上传 Apidoc

之前的用法是把所有的接口导入到默认模块中，按照文件夹来进行区分。<br/>
插件上传的时候需要选择模块，如果不单独设置，不会像原有那样可以选择文件夹。<br/>
因此这里将各模块单独独立出来，效果如下：<br/>

![输入图片说明](https://foruda.gitee.com/images/1753101309563059086/5c7de82c_4959041.png "屏幕截图")

新建模块：

![输入图片说明](https://foruda.gitee.com/images/1753101377513565932/7eb21bd1_4959041.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1753101387804054220/74421028_4959041.png "屏幕截图")

上传流程：

![输入图片说明](https://foruda.gitee.com/images/1753102049972873779/9ffb73cf_4959041.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1753101460286937773/c718468e_4959041.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1753102310528079364/80c0af60_4959041.png "屏幕截图")

查看控制台输出与文档：

![输入图片说明](https://foruda.gitee.com/images/1753102387726090214/16aae4ab_4959041.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1753102411755563077/354c132e_4959041.png "屏幕截图")

### 5. 插件配置

![输入图片说明](https://foruda.gitee.com/images/1753103060226305728/06889b21_4959041.png "屏幕截图")

更多使用方法请参考 [Apifox 官方文档](https://docs.apifox.com/doc-5743620)。