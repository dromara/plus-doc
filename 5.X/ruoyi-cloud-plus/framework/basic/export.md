# 导出功能
- - -

框架基于 `Apache Fesod(原EasyExcel)`（对 `Apache POI` 的封装与扩展）实现 Excel 导出。

[Apache Fesod 文档地址](https://fesod.apache.org/)

## 使用流程

### 1. 定义导出实体

以 `SysUserExportVo` 为例：

```java
/**
 * 用户ID
 */
@ExcelProperty(value = "用户序号")
private Long userId;

/**
 * 用户性别
 */
@ExcelProperty(value = "用户性别", converter = ExcelDictConvert.class)
@ExcelDictFormat(dictType = "sys_user_sex")
private String sex;

/**
 * 帐号状态（0正常 1停用）
 */
@ExcelProperty(value = "帐号状态", converter = ExcelDictConvert.class)
@ExcelDictFormat(dictType = "sys_normal_disable")
private String status;
```

说明：

- 使用 `@ExcelProperty` 标注需要导出的字段
- `value` 为表头字段名，`converter` 为转换器
- `@ExcelDictFormat` 为自定义注解，与字典转换器配合使用
- 建议导出对象单独定义，不要直接把数据库实体原样暴露到 Excel

### 2. 编写导出接口

以 `SysUserController#export` 为例：

```java
@PostMapping("/export")
public void export(SysUserBo user, HttpServletResponse response) {
    List<SysUserVo> list = userService.selectUserList(user);
    List<SysUserExportVo> listVo = MapstructUtils.convert(list, SysUserExportVo.class);
    ExcelUtil.exportExcel(listVo, "用户数据", SysUserExportVo.class, response);
}
```

补充说明：
- 常见做法是 `Vo -> ExportVo` 再导出，这样便于控制列顺序、字段脱敏和字典转换
- 导出接口通常是直接写 `HttpServletResponse` 输出流，因此方法返回值一般不再包装成 `R<?>`
- 前端按钮权限通常会对应 `xxx:export`

## 框架工具说明

### 1. 字典转换器

`ExcelDictConvert` 与 `@ExcelDictFormat` 搭配使用。

```java
@ExcelProperty(value = "用户性别", converter = ExcelDictConvert.class)
@ExcelDictFormat(dictType = "sys_user_sex")
private String sex;
```

也可使用表达式：

```java
@ExcelProperty(value = "用户性别", converter = ExcelDictConvert.class)
@ExcelDictFormat(readConverterExp="0=男,1=女,2=未知", separator=",")
private String sex;
```

`@ExcelDictFormat` 属性说明：

| 属性名称             | 类型     | 默认值 | 说明                       |
|------------------|--------|-----|--------------------------|
| dictType         | String | ""  | 字典 type（如：sys_user_sex）  |
| readConverterExp | String | ""  | 读取内容转表达式（如：0=男,1=女,2=未知） |
| separator        | String | "," | 表达式分隔符                   |

### 2. 枚举转换器

```java
@ExcelProperty(value = "用户类型", index = 1, converter = ExcelEnumConvert.class)
@ExcelEnumFormat(enumClass = UserStatus.class, textField = "info")
private String userStatus;
```

`@ExcelEnumFormat` 属性说明：

| 属性名称      | 类型         | 默认值  | 说明           |
|-----------|------------|------|--------------|
| enumClass | Enum Class | -    | 枚举类          |
| codeField | String     | code | 枚举中的 code 字段 |
| textField | String     | text | 枚举中的文本字段     |

### 3. 合并单元格

`@CellMerge` 用于合并相同列数据，需结合 `CellMergeStrategy` 使用。

```java
@CellMerge
@ExcelProperty(value = "部门id")
private Long deptId;
```

`@CellMerge` 属性说明：

| 属性名称    | 类型       | 默认值 | 说明          |
|---------|----------|-----|-------------|
| index   | int      | -1  | 合并列下标（建议默认） |
| mergeBy | String[] | {}  | 依赖字段名称      |

导出时开启合并：

```java
ExcelUtil.exportExcel(list, "测试单表", TestDemoVo.class, true, response);
```

![输入图片说明](https://foruda.gitee.com/images/1700128921644543994/e8d4704f_1766278.png "屏幕截图")

### 4. 复杂导出示例

`TestExcelController` 提供多种导出示例：

- 单列表多数据导出（模板导出）
- 多列表多数据导出（模板导出）
- 导出下拉框（`ExcelDictFormat` 默认下拉）

模板位置：`ruoyi-modules/ruoyi-demo/src/main/resources/excel/`

这些模板更适合作为结构示例参考，复杂业务仍建议按自己的导出字段和样式重新整理。

![输入图片说明](https://foruda.gitee.com/images/1700124852002972562/d9f57a8c_4959041.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1700124885532359879/0d011d05_4959041.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1700125025931981176/105dbaaa_4959041.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1700125054011300002/71869c1d_4959041.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1700125265411678973/7f767719_4959041.png "屏幕截图")

## 常用注解

| 类型  | 注解名称                    | 使用举例                                                        | 说明                         |
|-----|-------------------------|-------------------------------------------------------------|----------------------------|
| 格式化 | @DateTimeFormat         | @DateTimeFormat(value=格式化值)                                 | 日期格式化                      |
| 格式化 | @NumberFormat           | @NumberFormat(value=格式化值, roundingMode=舍入模式)                | 数值格式化                      |
| 样式  | @ColumnWidth            | @ColumnWidth(value=值)                                       | 列宽                         |
| 样式  | @ContentFontStyle       | @ContentFontStyle(color=颜色)                                 | 字体样式                       |
| 样式  | @ContentLoopMerge       | @ContentLoopMerge(eachRow=行值, columnExtend=列值)              | 循环合并区域                     |
| 样式  | @ContentRowHeight       | @ContentRowHeight(value=值)                                  | 行高                         |
| 样式  | @ContentStyle           | -                                                           | 单元格样式                      |
| 样式  | @HeadFontStyle          | @HeadFontStyle(color=颜色)                                    | 表头字体样式                     |
| 样式  | @HeadRowHeight          | @HeadRowHeight(value=值)                                     | 表头行高                       |
| 样式  | @HeadStyle              | -                                                           | 表头样式                       |
| 样式  | @OnceAbsoluteMerge      | @OnceAbsoluteMerge(...)                                     | 合并单元格                      |
| 属性  | @ExcelIgnore            | @ExcelIgnore                                                | 忽略字段                       |
| 属性  | @ExcelIgnoreUnannotated | @ExcelIgnoreUnannotated                                     | 仅处理标注 `@ExcelProperty` 的字段 |
| 属性  | @ExcelProperty          | @ExcelProperty(value=值, order=排序值, index=下标, converter=转换器) | 字段映射与排序                    |

## 扩展说明

### 自定义转换器

实现 `com.alibaba.excel.converters.Converter`：

![输入图片说明](https://foruda.gitee.com/images/1700104014304819918/33eb0c42_4959041.png "屏幕截图")

转换方法示例：

![输入图片说明](https://foruda.gitee.com/images/1700104426131801297/72931ef0_4959041.png "屏幕截图")

## 更多功能

更多导出能力请参考 [Apache Fesod 官方文档](https://fesod.apache.org/)。
