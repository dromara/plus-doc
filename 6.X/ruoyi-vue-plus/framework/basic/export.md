# 导出功能
- - -

框架基于 `Apache Fesod(原EasyExcel)`（对 `Apache POI` 的封装与扩展）实现 Excel 导出。

[Apache Fesod 文档地址](https://fesod.apache.org/)

核心源码位置：

```text
ruoyi-common/ruoyi-common-excel
```

## 基础导出

定义导出对象时，使用 Fesod 注解描述列信息，建议加 `@ExcelIgnoreUnannotated`，只导出显式标注的字段。

```java
@Data
@ExcelIgnoreUnannotated
public class UserExportVo {

    @ExcelProperty(value = "用户昵称", index = 0)
    private String nickName;

    @ExcelProperty(value = "性别", index = 1, converter = ExcelDictConvert.class)
    @ExcelDictFormat(dictType = "sys_user_gender")
    private String gender;

    @ExcelProperty(value = "用户类型", index = 2, converter = ExcelEnumConvert.class)
    @ExcelEnumFormat(enumClass = UserStatus.class, textField = "info")
    private String userStatus;
}
```

接口中直接写入 `HttpServletResponse`：

```java
@PostMapping("/export")
public void export(UserBo bo, HttpServletResponse response) {
    List<UserExportVo> list = userService.queryExportList(bo);

    ExcelBuilder.of(list, UserExportVo.class)
        .sheetName("用户数据")
        .toResponse(response);
}
```

常用链式配置：

```java
ExcelBuilder.of(list, UserExportVo.class)
    .sheetName("用户数据")
    .needHead(true)
    .automaticMergeHead(true)
    .includeFields(List.of("nickName", "gender"))
    .excludeFields(List.of("remark"))
    .columnWidth(20)
    .rowHeight((short) 22, (short) 18)
    .password("123456")
    .toResponse(response);
```

## 合并单元格

字段上使用 `@CellMerge`，导出时调用 `.merge()` 注册合并策略。

```java
@CellMerge
@ExcelProperty(value = "部门名称", index = 0)
private String deptName;
```

```java
ExcelBuilder.of(list, UserExportVo.class)
    .sheetName("用户数据")
    .merge()
    .toResponse(response);
```

`@CellMerge(mergeBy = {"deptName"})` 可以指定依赖字段，避免只按当前列值合并造成错位。

## 下拉框

字典和枚举字段会通过 `ExcelDownHandler` 自动处理为下拉选项：

```java
@ExcelProperty(value = "性别", index = 2, converter = ExcelDictConvert.class)
@ExcelDictFormat(dictType = "sys_user_gender")
private String gender;
```

业务动态下拉有两种方式。

方式一：字段上使用 `@ExcelDynamicOptions`：

```java
public class DeptOptions implements ExcelOptionsProvider {
    @Override
    public Set<String> getOptions() {
        return Set.of("研发部", "财务部", "市场部");
    }
}

@ExcelProperty(value = "部门", index = 3)
@ExcelDynamicOptions(providerClass = DeptOptions.class)
private String deptName;
```

方式二：接口中构造 `DropDownOptions`，适合级联下拉：

```java
DropDownOptions provinceToCity = DropDownOptions.buildLinkedOptions(
    provinceList,
    5,
    cityList,
    6,
    Province::getId,
    City::getPid,
    item -> DropDownOptions.createOptionValue(item.getName(), item.getId())
);

ExcelBuilder.of(list, ExportDemoVo.class)
    .sheetName("下拉框示例")
    .options(List.of(provinceToCity))
    .toResponse(response);
```

`DropDownOptions.createOptionValue()` 会把显示值和业务 ID 拼成合法选项；导入时可用 `DropDownOptions.analyzeOptionValue()` 解析回来。

## 批注和必填

`DataWriteHandler` 会处理框架扩展注解：

```java
@ExcelRequired
@ExcelNotation("手机号必须唯一")
@ExcelProperty(value = "手机号", index = 4)
private String phoneNumber;
```

说明：

- `@ExcelRequired` 会把表头字体标红
- `@ExcelNotation` 会给表头增加批注
- 两个注解仅适用于单层表头

## 自定义导出

需要分批写、同一 sheet 多次写、多个 sheet 或 table 时，使用 `ExcelBuilder.writer()`。

```java
ExcelBuilder.writer(UserExportVo.class)
    .sheetName("自定义导出")
    .toResponse(response, wrapper -> {
        WriteSheet sheet = ExcelWriterWrapper.sheetBuilder("用户数据").build();

        wrapper.write(firstPageList, sheet);
        wrapper.write(secondPageList, sheet);

        WriteSheet otherSheet = ExcelWriterWrapper.sheetBuilder("其他数据").build();
        wrapper.write(otherList, otherSheet);
    });
```

`ExcelWriterWrapper` 只暴露安全的 `write`、`fill`、`buildSheet`、`buildTable` 等方法，避免业务代码直接关闭底层 `ExcelWriter` 或响应流。

## ZIP 分页导出

数据量较大且需要拆成多个 Excel 文件时：

```java
ExcelBuilder.of(list, UserExportVo.class)
    .sheetName("用户数据")
    .zip(1000)
    .toResponse(response);
```

当分片数量大于 1 时会输出 zip；只有一个分片时自动按普通 xlsx 输出。

## 模板导出

模板文件放在 `resources/excel/` 下，模板语法使用 Fesod 填充语法。

单列表：

```java
ExcelBuilder.template("excel/单列表.xlsx")
    .filename("单列表")
    .data(list)
    .toResponse(response);
```

多列表：

```java
Map<String, Object> data = new HashMap<>();
data.put("map", titleMap);
data.put("data1", list1);
data.put("data2", list2);

ExcelBuilder.template("excel/多列表.xlsx")
    .filename("多列表")
    .multiList(data)
    .toResponse(response);
```

多 sheet：

```java
List<Map<String, Object>> sheets = List.of(
    Map.of("data1", list1),
    Map.of("data2", list2)
);

ExcelBuilder.template("excel/多sheet列表.xlsx")
    .filename("多sheet列表")
    .multiSheet(sheets)
    .toResponse(response);
```

参考示例：

```text
ruoyi-modules/ruoyi-demo/src/main/java/org/dromara/demo/controller/TestExcelController.java
ruoyi-modules/ruoyi-demo/src/main/java/org/dromara/demo/service/impl/ExportExcelServiceImpl.java
ruoyi-modules/ruoyi-demo/src/main/resources/excel/
```
