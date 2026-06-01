# 关于如何创建新模块
- - -

## 快速方式

参考 `ruoyi-demo` 模块直接复制。

补充说明：

- 单体版本新增的是“业务模块”，通常作为普通 Maven 模块接入主应用，而不是再单独起一个新服务。
- 如果只是增加一组业务表、Mapper、Service、Controller，直接复制 `ruoyi-demo` 的目录结构最省事。

## 必要改动

需要修改以下位置：

- 父 `pom.xml`
- `ruoyi-admin` 模块 `pom.xml`

![输入图片说明](https://foruda.gitee.com/images/1719814203987728184/6940ecf8_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1719814254968294155/70fe6d77_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1719814280768521481/14fb11cd_1766278.png "屏幕截图")

补充说明：

1. 在父 `pom.xml` 中声明新模块。
2. 在 `ruoyi-admin` 的 `pom.xml` 中引入新模块依赖，保证主应用启动时能扫描到该模块。
3. 同步修改模块名、包名、artifactId、注释说明，避免后续生成代码或接口文档出现混淆。
4. 如果模块里有自己的 `mapper.xml`、`domain`、`mapper` 包结构，包名尽量仍保持在 `org.dromara.**` 约定范围内，避免超出默认扫描规则。
5. 新模块接入后，前端菜单、权限标识、接口地址仍需要另外补齐。

## 注意事项

如果是不同包名的模块，需要同步修改配置：

![输入图片说明](https://foruda.gitee.com/images/1719813861680271619/82435586_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1692006501957936219/059f8526_1766278.png "屏幕截图")

补充说明：

- 如果你的包路径不再满足默认的 `org.dromara.**.mapper`、`org.dromara.**.domain` 规则，需要同步调整 MyBatis Plus 扫描配置。
- 复制模块后先确认能正常启动，再逐步清理示例代码、权限字符、菜单路由，效率比“一次性重命名全部内容”更高。
