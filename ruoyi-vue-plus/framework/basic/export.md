# 导出功能

- - -

在本框架中引入了 `Easy Excel` 依赖（对 `Apache POI`进行了封装以及扩展），可以对数据进行导出操作（即写 Excel）。

## 导出功能使用说明

### 步骤一：定义导出实体对象

以框架中 `SysUserExportVo` 为例：

```Java
    /**
     * 用户ID
     */
    @ExcelProperty(value = "用户序号")
    private Long userId;

    /**
     * 用户账号
     */
    @ExcelProperty(value = "登录名称")
    private String userName;

    /**
     * 用户昵称
     */
    @ExcelProperty(value = "用户名称")
    private String nickName;

    /**
     * 用户邮箱
     */
    @ExcelProperty(value = "用户邮箱")
    private String email;

    /**
     * 手机号码
     */
    @ExcelProperty(value = "手机号码")
    private String phonenumber;

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

> 说明：<br>
> 1. 使用 `@ExcelProperty` 注解标注需要导出的属性。
> 2. 注解 `@ExcelProperty` 中 `value` 属性代表表格头部标题字段，`converter` 代表使用的转换器，后面会详细说明。
> 3. 注解 `@ExcelDictFormat` 为自定义注解，与自定义转换器结合使用，同样在后面进行详细说明。

### 步骤二：使用导出方法

```Java
    /**
     * 导出用户列表
     */
    @PostMapping("/export")
    public void export(SysUserBo user, HttpServletResponse response) {
        // 根据参数查询导出的用户列表数据
        List<SysUserVo> list = userService.selectUserList(user);
        // 将列表转换为导出对象列表
        List<SysUserExportVo> listVo = MapstructUtils.convert(list, SysUserExportVo.class);
        // 导出方法
        ExcelUtil.exportExcel(listVo, "用户数据", SysUserExportVo.class, response);
    }
```

> 说明：<br>
> 使用 `ExcelUtil.exportExcel` 方法完成导出功能，上述 Demo 传入参数分别是：导出对象集合，Excel sheet 表名称，导出对象类型，response。

## Easy Excel 常用注解

`Easy Excel` 提供了丰富的注解可以对导出对象进行定制化操作，这里的注解说明针对的是原生注解，自定义注解会结合转换器一起进行说明。

| 类型    | 注解名称                    | 使用举例                                                                                                       | 说明                                                                                                       |
|-------|-------------------------|------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| 格式化注解 | @DateTimeFormat         | @DateTimeFormat(value=格式化值)                                                                                | 对字符串进行日期格式化 (参照 `java.text.SimpleDateFormat` 书写即可)                                                       |
| 格式化注解 | @NumberFormat           | @NumberFormat(value=格式化值, roundingMode=舍入模式)                                                               | 对字符串进行数值格式化 (参照 `java.text.DecimalFormat` 书写即可, `roundingMode` 默认 `RoundingMode.HALF_UP`)                |
| 样式注解  | @ColumnWidth            | @ColumnWidth(value=值)                                                                                      | 设置列宽                                                                                                     |
| 样式注解  | @ContentFontStyle       | @ContentFontStyle(color=颜色)                                                                                | 可以设置字体类型，颜色，粗细，是否斜体，下划线等，具体可查看注解 `@ContentFontStyle`                                                     |
| 样式注解  | @ContentLoopMerge       | @ContentLoopMerge(eachRow=行值, columnExtend=列值)                                                             | 设置循环合并的区域                                                                                                |
| 样式注解  | @ContentRowHeight       | @ContentRowHeight(value=值)                                                                                 | 设置内容行高                                                                                                   |
| 样式注解  | @ContentStyle           | -                                                                                                          | 设置单元格样式，具体可查看注解 `@ContentStyle`                                                                          |
| 样式注解  | @HeadFontStyle          | @HeadFontStyle(color=颜色)                                                                                   | 设置表头字体格式，类似 `@ContentFontStyle`，具体可查看注解 `@HeadFontStyle`                                                 |
| 样式注解  | @HeadRowHeight          | @HeadRowHeight(value=值)                                                                                    | 设置表头行高                                                                                                   |
| 样式注解  | @HeadStyle              | -                                                                                                          | 设置表头样式，具体可查看注解 `@HeadStyle`                                                                              |
| 样式注解  | @OnceAbsoluteMerge      | @OnceAbsoluteMerge(firstRowIndex=开始行下标, lastRowIndex=结束行下标, firstColumnIndex=开始列下标, lastColumnIndex=结束列下标) | 根据设置值合并单元格                                                                                               |
| 属性注解  | @ExcelIgnore            | @ExcelIgnore                                                                                               | 导出忽略该字段                                                                                                  |
| 属性注解  | @ExcelIgnoreUnannotated | @ExcelIgnoreUnannotated                                                                                    | 默认不管加不加 `@ExcelProperty` 的注解的所有字段都会参与读写，加了 `@ExcelIgnoreUnannotated` 注解以后，不加 `@ExcelProperty` 注解的字段就不会参与 |
| 属性注解  | @ExcelProperty          | @ExcelProperty(value=值, order=排序值, index=下标, converter=转换器)                                                | 默认按照对象属性顺序导出，如果设置了 `order` 以及 `index`，优先级 `index` > `order` > 默认；converter 可以自定义                         |

## 扩展使用

### 自定义转换器
由于业务需要，原生注解不一定能够符合需要，因而衍生出了自定义转换器。能够实现定制化的内容转换需要。 以下以框架中的字典转换器 `ExcelDictConvert` 为例进行说明。

#### 实现目的
字典转换器 `ExcelDictConvert`，顾名思义是对字典值进行转换。

例如用户性别字典 `sys_user_sex`，在数据库中存储的值为 0，1，2，导出时需要转换为对应的值：男，女，未知。

#### 使用方式
字典转换器使用了自定义注解 `@ExcelDictFormat` 配合使用。

有两种定义方式：
1. 使用字典类型定义 
```Java
@ExcelDictFormat(dictType="sys_user_sex")
```
> 说明：字典类型需要和字典管理中的类型对应。

2. 使用表达式
```Java
@ExcelDictFormat(readConverterExp="0=男,1=女,2=未知", separator=",")
```
> 说明：
> 1. `readConverterExp` 为表达式内容，`separator` 为表达式分隔符。
> 2. `separator` 默认值为 `,`，此处可以省略，如果表达式分隔符不同则需要显式声明。
 
_**注：自定义转换器并非一定需要自定义注解，也可以针对已有的注解进行自定义转换实现。**_

#### 自定义转换器实现
自定义转换器需要实现 `com.alibaba.excel.converters.Converter` 接口，实现接口中的方法。

![输入图片说明](https://foruda.gitee.com/images/1700104014304819918/33eb0c42_4959041.png "屏幕截图")

转换方法 `ExcelDictConvert#convertToExcelData` ：

![输入图片说明](https://foruda.gitee.com/images/1700104426131801297/72931ef0_4959041.png "屏幕截图")

## 更多功能
更多导出功能使用可以参照 `Easy Excel` [官方文档](https://easyexcel.opensource.alibaba.com/docs/current/api/write)。