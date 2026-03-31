# 导入功能
- - -

框架基于 `Apache Fesod(原EasyExcel)`（对 `Apache POI` 的封装与扩展）实现 Excel 导入。

[Apache Fesod 文档地址](https://fesod.apache.org/)

## 使用流程

### 1. 定义导入实体

以 `SysUserImportVo` 为例：

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

- 使用 `@ExcelProperty` 标注需要导入的字段
- `value` 为表头字段名，`converter` 为转换器
- `@ExcelDictFormat` 为自定义注解，与字典转换器配合使用
- **对象禁止使用链式注解 `@Accessors(chain = true)`，否则可能找不到 setter**
- 建议导入对象单独定义，不要直接复用数据库实体或返回给前端的 `Vo`

### 2. 编写导入接口

以 `SysUserController#importData` 为例：

```java
@Log(title = "用户管理", businessType = BusinessType.IMPORT)
@SaCheckPermission("system:user:import")
@PostMapping(value = "/importData", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
public R<Void> importData(@RequestPart("file") MultipartFile file, boolean updateSupport) throws Exception {
    ExcelResult<SysUserImportVo> result = ExcelUtil.importExcel(
        file.getInputStream(),
        SysUserImportVo.class,
        new SysUserImportListener(updateSupport)
    );
    return R.ok(result.getAnalysis());
}
```

补充说明：
- `updateSupport` 这类参数通常用于控制“导入时是否允许更新已存在数据”
- 导入接口建议保留独立权限标识，例如 `system:user:import`
- 如果前端走默认 `plus-ui` 上传组件，接口通常需要使用 `multipart/form-data`

## 框架工具说明

### 1. 字典转换器

`ExcelDictConvert` 与 `@ExcelDictFormat` 搭配使用。

方式一：

```java
@ExcelProperty(value = "用户性别", converter = ExcelDictConvert.class)
@ExcelDictFormat(dictType = "sys_user_sex")
private String sex;
```

方式二：

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

`ExcelEnumConvert` 与 `@ExcelEnumFormat` 搭配使用：

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

### 3. 导入监听器

- `ExcelListener`：扩展 `ReadListener`，增加结果获取能力
- `DefaultExcelListener`：默认监听器，负责校验与异常处理
- `SysUserImportListener`：用户导入监听器
- `ExportDemoListener`：处理带下拉框的导入

一般业务导入逻辑都建议放在监听器里分批处理，而不是在 Controller 里直接逐行写入。

## 常用注解

| 类型  | 注解名称                    | 使用举例                                                        | 说明                         |
|-----|-------------------------|-------------------------------------------------------------|----------------------------|
| 格式化 | @DateTimeFormat         | @DateTimeFormat(value=格式化值)                                 | 日期格式化                      |
| 格式化 | @NumberFormat           | @NumberFormat(value=格式化值, roundingMode=舍入模式)                | 数值格式化                      |
| 属性  | @ExcelIgnore            | @ExcelIgnore                                                | 忽略字段                       |
| 属性  | @ExcelIgnoreUnannotated | @ExcelIgnoreUnannotated                                     | 仅处理标注 `@ExcelProperty` 的字段 |
| 属性  | @ExcelProperty          | @ExcelProperty(value=值, order=排序值, index=下标, converter=转换器) | 字段映射与排序                    |

## 扩展用法

### 自定义转换器

实现 `com.alibaba.excel.converters.Converter`：

![输入图片说明](https://foruda.gitee.com/images/1700104014304819918/33eb0c42_4959041.png "屏幕截图")

转换方法示例：

![输入图片说明](https://foruda.gitee.com/images/1700182975516396213/d3c020f9_4959041.png "屏幕截图")

### 自定义监听器

步骤建议：

1. 继承 `AnalysisEventListener` 并实现 `ExcelListener`
2. 显式使用构造函数（避免空指针）
3. 实现 `invoke` 与 `getExcelResult` 处理结果

如果导入量较大，建议在监听器中做分批落库、错误收集和结果汇总，避免一次性全部堆在内存里。

![输入图片说明](https://foruda.gitee.com/images/1700184652693497753/09333dac_4959041.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1700184759075616584/cf05b0ed_4959041.png "屏幕截图")

## 更多功能

更多导入能力请参考 [Apache Fesod 官方文档](https://fesod.apache.org/)。

