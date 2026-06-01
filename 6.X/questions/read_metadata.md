# unable to read meta-data for class xxx
- - -

## 常见原因

修改包名后，组件的 Spring SPI 配置文件未同步更新，导致类路径失效。

## 解决方案

更正组件包下的 spring spi 配置文件内的类包名

![输入图片说明](https://foruda.gitee.com/images/1668608724503582409/50a77b4b_1766278.jpeg "test.jpg")