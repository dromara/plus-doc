# 分页功能
- - -

## 适用版本

- 3.5.0 版本

## 功能说明

- 基于 `MyBatis-Plus` 分页插件实现
- 已开启分页合理化：页码溢出会返回第一页
- 用法与 MP 一致，可直接复用 MP 经验
- 常用入参为 `pageNum`、`pageSize`，也支持 `orderByColumn`、`isAsc` 排序

参考文档：[MP分页文档](https://baomidou.com/pages/97710a/)

![输入图片说明](https://foruda.gitee.com/images/1678977804058241635/b5cb362d_1766278.png "屏幕截图")

## 使用步骤

### 1. Controller 接收分页参数

使用 `PageQuery` 接收分页参数，具体字段可参考 `PageQuery` 类。

补充说明：
- `pageNum` 默认从 `1` 开始
- `pageSize` 不传时会按 `PageQuery` 默认值处理，前端列表页一般都会显式传入
- 排序参数示例：`orderByColumn=createTime`、`isAsc=desc`

![输入图片说明](https://foruda.gitee.com/images/1678977844048821356/1f994221_1766278.png "屏幕截图")

### 2. 构建 MP 分页对象

使用 `PageQuery#build()` 基于当前对象快速构建 MP 分页对象。

列表接口返回给前端时，通常直接使用 `TableDataInfo.build(pageResult)` 封装分页结果，前端表格组件可以直接复用这套返回结构。

![输入图片说明](https://foruda.gitee.com/images/1678977862816976499/b82c1638_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678977876194578744/eaa7b854_1766278.png "屏幕截图")

### 3. 自定义 SQL 分页

自定义 SQL 需要在 Mapper 方法**第一个参数**传入分页对象，返回值为分页结果。

![输入图片说明](https://foruda.gitee.com/images/1678977898181729571/6e102731_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678977906788451483/70979292_1766278.png "屏幕截图")

## 示例参数

- `pageNum=1`
- `pageSize=10`
- `orderByColumn=createTime`
- `isAsc=desc`

