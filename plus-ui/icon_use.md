# 使用图标

- - -

### 在页面中使用
**详情请参考ElementPlus文档**
* 直接使用ElementPlus中的图标
```html
<el-icon>
    <edit/>
</el-icon>
```

* 通过`:size`属性来调整图标大小(默认单位为px)
```html
<el-icon :size="20">
    <edit/>
</el-icon>
```

* 图标颜色
```html
<el-icon color="#409EFF">
    <edit/>
</el-icon>
```

### 在按钮中使用
* 可以通过设置`icon`属性来使用图标
```html
<el-button icon="el-icon-edit">编辑</el-button>
```

* 也可以直接使用图标组件
```html
<el-button>
    编辑
    <el-icon>
        <edit/>
    </el-icon>
</el-button>
```

### 在菜单中添加自定义的图标
1. 在阿里巴巴矢量图标库找到你想要的图标
2. 点击下载`svg`格式
3. 将下载好的`svg`文件放入 `src/assets/icons/svg`目录下
4. 在选择菜单图标时，选择你添加的图标即可