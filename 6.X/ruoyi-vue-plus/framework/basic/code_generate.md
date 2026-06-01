# 代码生成
- - -

## 模块位置

单体项目的代码生成模块：

```text
ruoyi-modules/ruoyi-gen
```

核心入口：

```text
controller/GenController.java
service/GenTableServiceImpl.java
resources/vm
```

控制器路径为：

```text
/tool/gen
```

## 接口路径

常用接口：

```text
GET    /tool/gen/list
GET    /tool/gen/{tableId}
GET    /tool/gen/db/list
GET    /tool/gen/column/{tableId}
POST   /tool/gen/importTable
PUT    /tool/gen
DELETE /tool/gen/{tableIds}
GET    /tool/gen/preview/{tableId}
GET    /tool/gen/download/{tableId}
GET    /tool/gen/synchDb/{tableId}
GET    /tool/gen/batchGenCode
GET    /tool/gen/getDataNames
```

导入表时会传入：

```text
tables   表名，多个用逗号分隔
dataName 数据源名称
```

`GenTableServiceImpl` 通过 `@DS("#dataName")` 切换到目标库读取表结构，并把 `dataName` 写入 `gen_table`。

## 使用步骤

1. 在 `application-*.yml` 的 `spring.datasource.dynamic.datasource` 中确认目标数据源存在。
2. 进入 `系统工具 -> 代码生成`。
3. 点击导入，选择数据源和数据表。
4. 编辑“基本信息、字段信息、生成信息”。
5. 预览代码，确认包名、模块名、业务名、权限标识和前端路径。
6. 下载代码或复制到项目中。
7. 表结构变化后使用“同步”重新读取字段。

## 字段规则

建议业务表沿用框架标准字段：

```text
create_by
create_time
update_by
update_time
del_flag
version
```

生成器会根据字段配置决定：

| 配置 | 影响范围 |
| --- | --- |
| 插入 / 编辑 | BO 校验和前端表单 |
| 列表 | VO 和列表列 |
| 查询 | 查询条件和搜索区域 |
| 查询方式 | 等值、模糊、范围等查询表达式 |
| 必填 | 后端校验和前端必填 |
| 显示类型 | 输入框、下拉框、日期、上传等组件 |
| 字典类型 | 字典回显和选项加载 |

## 树表

选择树表模板时必须正确配置：

```text
treeCode        当前节点主键字段
treeParentCode  父节点字段
treeName        节点展示字段
```

字段选错会导致前端层级、展开和回显异常。

## 使用注意

- 当前生成器以单表生成为主，不推荐直接生成复杂主子表。
- 已二次开发的模块不要直接覆盖，先预览或对比生成结果。
- “同步”只重新读取表结构，不会理解你手写的业务逻辑。
- 多数据源生成时，`dataName` 必须和动态数据源配置名一致。
