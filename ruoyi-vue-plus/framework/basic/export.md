# 导出功能

- - -

在本框架中引入了 `Easy Excel` 依赖（对 `Apache POI`进行了封装以及扩展），可以对数据进行导出操作（即写 Excel）。

## 导出功能使用流程说明

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

以框架中 `SysUserController#export` 方法为例：

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

## 框架工具使用说明

### 1：字典转换器

字典转换器 `ExcelDictConvert` 与自定义注解 `@ExcelDictFormat` 结合使用，标注在需要转换的属性上。

使用方式一：

```Java
    /**
     * 用户性别
     */
    @ExcelProperty(value = "用户性别", converter = ExcelDictConvert.class)
    @ExcelDictFormat(dictType = "sys_user_sex")
    private String sex;
```

使用方式二：

```Java
    /**
     * 用户性别
     */
    @ExcelProperty(value = "用户性别", converter = ExcelDictConvert.class)
    @ExcelDictFormat(readConverterExp="0=男,1=女,2=未知", separator=",")
    private String sex;
```

`@ExcelDictFormat` 注解属性说明：

| 属性名称             | 属性类型   | 默认值 | 说明                                |
|------------------|--------|-----|-----------------------------------|
| dictType         | String | ""  | 字典的type值 (如: sys_user_sex)        |
| readConverterExp | String | ""  | 读取内容转表达式 (如: 0=男,1=女,2=未知)        |
| separator        | String | "," | 与 readConverterExp 属性结合使用，表达式的分隔符 |

### 2：枚举转换器

字典转换器 `ExcelEnumConvert` 与自定义注解 `@ExcelEnumFormat` 结合使用，标注在需要转换的属性上。

使用方式：

```Java
    /**
     * 用户类型
     * </p>
     * 使用ExcelEnumFormat注解需要进行下拉选的部分
     */
    @ExcelProperty(value = "用户类型", index = 1, converter = ExcelEnumConvert.class)
    @ExcelEnumFormat(enumClass = UserStatus.class, textField = "info")
    private String userStatus;
```

`@ExcelEnumFormat` 注解属性说明：

| 属性名称      | 属性类型       | 默认值  | 说明                           |
|-----------|------------|------|------------------------------|
| enumClass | Enum Class | -    | 字典枚举类型                       |
| codeField | String     | code | 字典枚举类中对应的 code 属性名称，默认为 code |
| textField | String     | text | 字典枚举类中对应的 text 属性名称，默认为 text |

### 3：合并单元格

`@CellMerge` 注解用于合并相同的列数据，需要结合 `CellMergeStrategy` 策略使用，标注在需要转换的属性上。

使用方式：

步骤一：在属性标注 `@CellMerge` 注解：
```Java
    /**
     * 部门id
     */
    @CellMerge
    @ExcelProperty(value = "部门id")
    private Long deptId;
```

`@CellMerge` 注解属性说明：

| 属性名称  | 属性类型 | 默认值 | 说明             |
|-------|------|-----|----------------|
| index | int  | -1  | 合并列的下标，建议使用默认值 |

步骤二：导出方法开启合并：
```Java
    /**
     * 导出测试单表列表
     */
    @PostMapping("/export")
    public void export(@Validated TestDemoBo bo, HttpServletResponse response) {
        List<TestDemoVo> list = testDemoService.queryList(bo);
        // 参数 true 表示开启合并单元格策略
        ExcelUtil.exportExcel(list, "测试单表", TestDemoVo.class, true, response);
    } 
```

### 4：复杂 Excel 导出示例
`TestExcelController` 提供了几种导出示例，如果需要可以参照相应方法进行导出。

#### 4.1：单列表多数据导出（模板导出）

模板内容：

![输入图片说明](https://foruda.gitee.com/images/1700124852002972562/d9f57a8c_4959041.png "屏幕截图")

模板位置：`ruoyi-modules/ruoyi-demo/src/main/resources/excel/`

导出示例代码：

```Java
    /**
     * 单列表多数据
     */
    @GetMapping("/exportTemplateOne")
    public void exportTemplateOne(HttpServletResponse response) {
        Map<String, String> map = new HashMap<>();
        map.put("title", "单列表多数据");
        map.put("test1", "数据测试1");
        map.put("test2", "数据测试2");
        map.put("test3", "数据测试3");
        map.put("test4", "数据测试4");
        map.put("testTest", "666");
        List<TestObj> list = new ArrayList<>();
        list.add(new TestObj("单列表测试1", "列表测试1", "列表测试2", "列表测试3", "列表测试4"));
        list.add(new TestObj("单列表测试2", "列表测试5", "列表测试6", "列表测试7", "列表测试8"));
        list.add(new TestObj("单列表测试3", "列表测试9", "列表测试10", "列表测试11", "列表测试12"));
        ExcelUtil.exportTemplate(CollUtil.newArrayList(map, list), "单列表.xlsx", "excel/单列表.xlsx", response);
    }
```

导出结果：

![输入图片说明](https://foruda.gitee.com/images/1700124885532359879/0d011d05_4959041.png "屏幕截图")

#### 4.2：多列表多数据导出（模板导出）

模板内容：

![输入图片说明](https://foruda.gitee.com/images/1700125025931981176/105dbaaa_4959041.png "屏幕截图")

模板位置：`ruoyi-modules/ruoyi-demo/src/main/resources/excel/`

导出示例代码：

```Java
    /**
     * 多列表多数据
     */
    @GetMapping("/exportTemplateMuliti")
    public void exportTemplateMuliti(HttpServletResponse response) {
        Map<String, String> map = new HashMap<>();
        map.put("title1", "标题1");
        map.put("title2", "标题2");
        map.put("title3", "标题3");
        map.put("title4", "标题4");
        map.put("author", "Lion Li");
        List<TestObj1> list1 = new ArrayList<>();
        list1.add(new TestObj1("list1测试1", "list1测试2", "list1测试3"));
        list1.add(new TestObj1("list1测试4", "list1测试5", "list1测试6"));
        list1.add(new TestObj1("list1测试7", "list1测试8", "list1测试9"));
        List<TestObj1> list2 = new ArrayList<>();
        list2.add(new TestObj1("list2测试1", "list2测试2", "list2测试3"));
        list2.add(new TestObj1("list2测试4", "list2测试5", "list2测试6"));
        List<TestObj1> list3 = new ArrayList<>();
        list3.add(new TestObj1("list3测试1", "list3测试2", "list3测试3"));
        List<TestObj1> list4 = new ArrayList<>();
        list4.add(new TestObj1("list4测试1", "list4测试2", "list4测试3"));
        list4.add(new TestObj1("list4测试4", "list4测试5", "list4测试6"));
        list4.add(new TestObj1("list4测试7", "list4测试8", "list4测试9"));
        list4.add(new TestObj1("list4测试10", "list4测试11", "list4测试12"));
        Map<String, Object> multiListMap = new HashMap<>();
        multiListMap.put("map", map);
        multiListMap.put("data1", list1);
        multiListMap.put("data2", list2);
        multiListMap.put("data3", list3);
        multiListMap.put("data4", list4);
        ExcelUtil.exportTemplateMultiList(multiListMap, "多列表.xlsx", "excel/多列表.xlsx", response);
    }
```

导出结果：

![输入图片说明](https://foruda.gitee.com/images/1700125054011300002/71869c1d_4959041.png "屏幕截图")

#### 4.3：导出下拉框

导出示例代码：

```Java
    /**
     * 导出下拉框
     *
     * @param response /
     */
    @GetMapping("/exportWithOptions")
    public void exportWithOptions(HttpServletResponse response) {
        exportExcelService.exportWithOptions(response);
    }
```

```Java
    @Override
    public void exportWithOptions(HttpServletResponse response) {
        // 创建表格数据，业务中一般通过数据库查询
        List<ExportDemoVo> excelDataList = new ArrayList<>();
        for (int i = 0; i < 3; i++) {
            // 模拟数据库中的一条数据
            ExportDemoVo everyRowData = new ExportDemoVo();
            everyRowData.setNickName("用户-" + i);
            everyRowData.setUserStatus(UserStatus.OK.getCode());
            everyRowData.setGender("1");
            everyRowData.setPhoneNumber(String.format("175%08d", i));
            everyRowData.setEmail(String.format("175%08d", i) + "@163.com");
            everyRowData.setProvinceId(i);
            everyRowData.setCityId(i);
            everyRowData.setAreaId(i);
            excelDataList.add(everyRowData);
        }

        // 通过@ExcelIgnoreUnannotated配合@ExcelProperty合理显示需要的列
        // 并通过@DropDown注解指定下拉值，或者通过创建ExcelOptions来指定下拉框
        // 使用ExcelOptions时建议指定列index，防止出现下拉列解析不对齐

        // 首先从数据库中查询下拉框内的可选项
        // 这里模拟查询结果
        List<DemoCityData> provinceList = getProvinceList(),
            cityList = getCityList(provinceList),
            areaList = getAreaList(cityList);
        int provinceIndex = 5, cityIndex = 6, areaIndex = 7;

        DropDownOptions provinceToCity = DropDownOptions.buildLinkedOptions(
            provinceList,
            provinceIndex,
            cityList,
            cityIndex,
            DemoCityData::getId,
            DemoCityData::getPid,
            everyOptions -> DropDownOptions.createOptionValue(
                everyOptions.getName(),
                everyOptions.getId()
            )
        );

        DropDownOptions cityToArea = DropDownOptions.buildLinkedOptions(
            cityList,
            cityIndex,
            areaList,
            areaIndex,
            DemoCityData::getId,
            DemoCityData::getPid,
            everyOptions -> DropDownOptions.createOptionValue(
                everyOptions.getName(),
                everyOptions.getId()
            )
        );

        // 把所有的下拉框存储
        List<DropDownOptions> options = new ArrayList<>();
        options.add(provinceToCity);
        options.add(cityToArea);

        // 到此为止所有的下拉框可选项已全部配置完毕

        // 接下来需要将Excel中的展示数据转换为对应的下拉选
        List<ExportDemoVo> outList = StreamUtils.toList(excelDataList, everyRowData -> {
            // 只需要处理没有使用@ExcelDictFormat注解的下拉框
            // 一般来说，可以直接在数据库查询即查询出省市县信息，这里通过模拟操作赋值
            everyRowData.setProvince(buildOptions(provinceList, everyRowData.getProvinceId()));
            everyRowData.setCity(buildOptions(cityList, everyRowData.getCityId()));
            everyRowData.setArea(buildOptions(areaList, everyRowData.getAreaId()));
            return everyRowData;
        });

        ExcelUtil.exportExcel(outList, "下拉框示例", ExportDemoVo.class, response, options);
    }
```

导出结果：

![输入图片说明](https://foruda.gitee.com/images/1700125265411678973/7f767719_4959041.png "屏幕截图")

### 5：ExcelUtil 工具类

`ExcelUtil` 工具类中有常用的 Excel 方法。包括直接导出以及模板导出。

#### 直接导出主要方法
```Java
    /**
     * 导出excel
     *
     * @param list      导出数据集合
     * @param sheetName 工作表的名称
     * @param clazz     实体类
     * @param merge     是否合并单元格
     * @param os        输出流
     */
    public static <T> void exportExcel(List<T> list, String sheetName, Class<T> clazz, boolean merge,
                                       OutputStream os, List<DropDownOptions> options) {
        ExcelWriterSheetBuilder builder = EasyExcel.write(os, clazz)
            .autoCloseStream(false)
            // 自动适配
            .registerWriteHandler(new LongestMatchColumnWidthStyleStrategy())
            // 大数值自动转换 防止失真
            .registerConverter(new ExcelBigNumberConvert())
            .sheet(sheetName);
        if (merge) {
            // 合并处理器
            builder.registerWriteHandler(new CellMergeStrategy(list, true));
        }
        // 添加下拉框操作
        builder.registerWriteHandler(new ExcelDownHandler(options));
        builder.doWrite(list);
    }
```

#### 单表多数据模板导出方法
```Java
    /**
     * 单表多数据模板导出 模板格式为 {.属性}
     *
     * @param templatePath 模板路径 resource 目录下的路径包括模板文件名
     *                     例如: excel/temp.xlsx
     *                     重点: 模板文件必须放置到启动类对应的 resource 目录下
     * @param data         模板需要的数据
     * @param os           输出流
     */
    public static void exportTemplate(List<Object> data, String templatePath, OutputStream os) {
        ClassPathResource templateResource = new ClassPathResource(templatePath);
        ExcelWriter excelWriter = EasyExcel.write(os)
            .withTemplate(templateResource.getStream())
            .autoCloseStream(false)
            // 大数值自动转换 防止失真
            .registerConverter(new ExcelBigNumberConvert())
            .build();
        WriteSheet writeSheet = EasyExcel.writerSheet().build();
        if (CollUtil.isEmpty(data)) {
            throw new IllegalArgumentException("数据为空");
        }
        // 单表多数据导出 模板格式为 {.属性}
        for (Object d : data) {
            excelWriter.fill(d, writeSheet);
        }
        excelWriter.finish();
    }
```

#### 多表多数据模板导出方法
```Java
    /**
     * 多表多数据模板导出 模板格式为 {key.属性}
     *
     * @param templatePath 模板路径 resource 目录下的路径包括模板文件名
     *                     例如: excel/temp.xlsx
     *                     重点: 模板文件必须放置到启动类对应的 resource 目录下
     * @param data         模板需要的数据
     * @param os           输出流
     */
    public static void exportTemplateMultiList(Map<String, Object> data, String templatePath, OutputStream os) {
        ClassPathResource templateResource = new ClassPathResource(templatePath);
        ExcelWriter excelWriter = EasyExcel.write(os)
            .withTemplate(templateResource.getStream())
            .autoCloseStream(false)
            // 大数值自动转换 防止失真
            .registerConverter(new ExcelBigNumberConvert())
            .build();
        WriteSheet writeSheet = EasyExcel.writerSheet().build();
        if (CollUtil.isEmpty(data)) {
            throw new IllegalArgumentException("数据为空");
        }
        for (Map.Entry<String, Object> map : data.entrySet()) {
            // 设置列表后续还有数据
            FillConfig fillConfig = FillConfig.builder().forceNewRow(Boolean.TRUE).build();
            if (map.getValue() instanceof Collection) {
                // 多表导出必须使用 FillWrapper
                excelWriter.fill(new FillWrapper(map.getKey(), (Collection<?>) map.getValue()), fillConfig, writeSheet);
            } else {
                excelWriter.fill(map.getValue(), writeSheet);
            }
        }
        excelWriter.finish();
    }
```

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

## 扩展说明

### 自定义转换器实现

由于业务需要，原生注解不一定能够符合需要，因而衍生出了自定义转换器。能够实现定制化的内容转换需要。
以下以框架中的字典转换器 `ExcelDictConvert` 为例进行说明。

字典转换器 `ExcelDictConvert`，字典转换器使用了自定义注解 `@ExcelDictFormat` 配合使用。

_**注：自定义转换器并非一定需要自定义注解，也可以针对已有的注解进行自定义转换实现。**_

#### 实现方式

自定义转换器需要实现 `com.alibaba.excel.converters.Converter` 接口，实现接口中的方法。

![输入图片说明](https://foruda.gitee.com/images/1700104014304819918/33eb0c42_4959041.png "屏幕截图")

转换方法 `ExcelDictConvert#convertToExcelData` ：

![输入图片说明](https://foruda.gitee.com/images/1700104426131801297/72931ef0_4959041.png "屏幕截图")

## 更多功能

更多导出功能使用可以参照 `Easy Excel` [官方文档](https://easyexcel.opensource.alibaba.com/docs/current/api/write)。