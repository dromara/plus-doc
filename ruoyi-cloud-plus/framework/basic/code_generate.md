# 代码生成
- - -
## 功能介绍

### 数据源配置

![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/110826_bf8dba86_1766278.png "屏幕截图.png")

后续版本 项目适配多种类型数据库 可以再代码生成页面切换<br>
填写对应的数据源名称 点击搜索按钮 即可切换到对应的数据源<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/110933_b011ea8f_1766278.png "屏幕截图.png")

### 导入数据表

点击导入按钮 会加载系统数据库所有的表<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/111212_75a30324_1766278.png "屏幕截图.png")

选择需要的表 点击确定即可<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/111312_dfca60f4_1766278.png "屏幕截图.png")<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/111331_bb16f75f_1766278.png "屏幕截图.png")

### 编辑表生成结构

点击表对应的编辑按钮<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/111400_d424f749_1766278.png "屏幕截图.png")

更改要生成表的数据<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/111458_d02c8555_1766278.png "屏幕截图.png")<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/111521_39f2d0d3_1766278.png "屏幕截图.png")

### 生成条件影响
![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/111556_8ae0b0e6_1766278.png "屏幕截图.png")


* `插入` `编辑` 影响生成 BO 类是否有该字段
* `列表` 影响生成 VO 类是否有该字段
* `查询` 影响页面是否有该字段的搜索框与后端代码是否生成对应的查询条件
* `查询方式` 影响生成查询条件的类型
* `必填` 影响 BO 类 与 页面是否强制校验
* `显示类型` 影响生成页面使用何种展示组件
* `字典类型` 影响页面是否生成字段关联

### 树表配置

编辑表生成信息 生成模板为 `树表` 填写对应数据即可<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/112210_c12c0e2a_1766278.png "屏幕截图.png")

### 主子表说明

框架不支持也不推荐使用主子表<br>
原因一般业务场景 基本都是一对N表 多表关联场景<br>
还有一些 主 => 子 <= 主 场景 需求很复杂 很少有单纯主子表场景出现<br>
另外主子表关联 很容易出现 笛卡尔积 或者数据错乱等问题 需要自行sql调优场景<br>
所有建议大家都按照 单表生成 自行编写业务逻辑

### 预览功能

配置好生成信息后 可以点击预览按钮<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/112635_cd58ab0c_1766278.png "屏幕截图.png")

系统会根据已经配置好的数据 生成对应的代码预览<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/112726_613d1f7d_1766278.png "屏幕截图.png")

可以再此处观察代码的生成结构和数据是否正确等

### 代码结构同步

实际开发中 难免会有表结构更改的需求<br>
这时可以使用 同步功能 点击同步按钮 即可与实时数据库表进行字段同步<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0421/112939_5198ebde_1766278.png "屏幕截图.png")
