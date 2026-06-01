# 导入功能
- - -

框架基于 `Apache Fesod(原EasyExcel)`（对 `Apache POI` 的封装与扩展）实现 Excel 导入。

[Apache Fesod 文档地址](https://fesod.apache.org/)

核心源码位置：

```text
ruoyi-common/ruoyi-common-excel
```

## 基础导入

定义导入对象：

```java
@Data
@ExcelIgnoreUnannotated
public class UserImportVo {

    @ExcelProperty(value = "用户昵称", index = 0)
    @NotBlank(message = "用户昵称不能为空")
    private String nickName;

    @ExcelProperty(value = "性别", index = 1, converter = ExcelDictConvert.class)
    @ExcelDictFormat(dictType = "sys_user_gender")
    @NotBlank(message = "性别不能为空")
    private String gender;

    @ExcelProperty(value = "手机号", index = 2)
    @NotBlank(message = "手机号不能为空")
    private String phoneNumber;
}
```

导入接口：

```java
@PostMapping(value = "/importData", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
public R<String> importData(@RequestPart("file") MultipartFile file) throws Exception {
    ExcelResult<UserImportVo> result = ExcelBuilder.read(file.getInputStream(), UserImportVo.class)
        .doRead();

    List<UserImportVo> list = result.getList();
    userService.importData(list);
    return R.ok(result.getAnalysis());
}
```

默认行为：

- 默认使用 `DefaultExcelListener`
- 默认执行 Validator 校验
- 默认 `failFast=true`，遇到异常立即终止读取
- 返回 `ExcelResult<T>`，可取 `getList()`、`getErrorList()`、`getAnalysis()`

## 读取配置

`ExcelBuilder.read(...)` 支持链式配置：

```java
ExcelResult<UserImportVo> result = ExcelBuilder.read(file.getInputStream(), UserImportVo.class)
    .sheetNo(0)
    .sheetName("用户")
    .headRowNumber(1)
    .ignoreEmptyRow(true)
    .autoTrim(true)
    .autoStrip(true)
    .validate(true)
    .failFast(false)
    .numRows(1000)
    .doRead();
```

常用方法说明：

| 方法 | 说明 |
| --- | --- |
| `sheetNo` | 读取指定 sheet 下标 |
| `sheetName` | 读取指定 sheet 名称 |
| `headRowNumber` | 表头行数 |
| `ignoreEmptyRow` | 是否忽略空行 |
| `autoTrim` | 是否自动 trim 字符串 |
| `autoStrip` | 是否清理不可见字符 |
| `validate` | 是否执行 Validator 校验 |
| `failFast` | 是否遇到异常立即终止 |
| `numRows` | 限制读取行数 |
| `registerConverter` | 注册自定义转换器 |

如果只需要同步读取对象集合：

```java
List<UserImportVo> list = ExcelBuilder.read(file.getInputStream(), UserImportVo.class)
    .doReadSync();
```

读取所有 sheet：

```java
ExcelResult<UserImportVo> result = ExcelBuilder.read(file.getInputStream(), UserImportVo.class)
    .doReadAll();
```

## 自定义监听器

复杂导入建议放在监听器里处理，例如分批落库、逐行转换、收集错误信息。

```java
public class UserImportListener extends DefaultExcelListener<UserImportVo> {

    public UserImportListener() {
        super(true, false);
    }

    @Override
    public void invoke(UserImportVo data, AnalysisContext context) {
        ValidatorUtils.validate(data);

        // 行级业务校验、转换、缓存或分批入库

        getExcelResult().getList().add(data);
    }
}
```

接口中指定监听器：

```java
ExcelResult<UserImportVo> result = ExcelBuilder.read(file.getInputStream(), UserImportVo.class)
    .listener(new UserImportListener())
    .doRead();
```

## 字典、枚举和级联下拉

字典导入：

```java
@ExcelProperty(value = "性别", index = 1, converter = ExcelDictConvert.class)
@ExcelDictFormat(dictType = "sys_user_gender")
private String gender;
```

枚举导入：

```java
@ExcelProperty(value = "用户类型", index = 2, converter = ExcelEnumConvert.class)
@ExcelEnumFormat(enumClass = UserStatus.class, textField = "info")
private String userStatus;
```

级联下拉导入时，导出端应使用 `DropDownOptions.createOptionValue()` 写出选项，导入端用 `analyzeOptionValue()` 解析：

```java
List<String> selected = DropDownOptions.analyzeOptionValue(data.getProvince());
if (selected.size() == 2) {
    String provinceId = selected.get(1);
}
```

完整示例参考：

```text
ruoyi-modules/ruoyi-demo/src/main/java/org/dromara/demo/listener/ExportDemoListener.java
```

## 注意事项

- 导入对象不要直接复用数据库实体，建议单独建 `ImportVo`
- 不要给导入对象使用链式 setter，否则 Fesod 可能找不到标准 setter
- 业务唯一性、外键存在性、跨行重复等校验建议在监听器中处理
- 大文件导入不要在 Controller 中一次性写复杂逻辑，优先使用监听器分批处理
- 自定义转换器包名使用 `org.apache.fesod.sheet.converters.Converter`
