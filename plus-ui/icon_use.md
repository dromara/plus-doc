# 使用图标

- - -

### 在页面中使用
**详情请参考ElementPlus文档**
* 直接使用 Element Plus 图标组件
```html
<el-icon>
    <edit/>
</el-icon>
```

* 通过 `:size` 属性调整图标大小（默认单位为 px）
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

补充说明：
- 当前项目已经在启动时全局注册 `@element-plus/icons-vue`，常见图标组件可直接使用
- 如果使用的是 SVG 业务图标，通常改用 `svg-icon`

### 在按钮中使用
* 可以通过 `icon` 属性使用图标组件
```html
<script setup lang="ts">
import { Edit } from '@element-plus/icons-vue'
</script>

<el-button :icon="Edit">编辑</el-button>
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

### 使用项目内 SVG 图标

项目内大量菜单、导航、登录页图标都使用 `svg-icon` 组件：

```html
<svg-icon icon-class="user" />
```

补充说明：
- `icon-class` 对应 `src/assets/icons/svg` 目录下的 svg 文件名
- 这种方式更适合菜单图标、品牌图标、自定义业务图标

### 在菜单中添加自定义的图标
1. 在阿里巴巴矢量图标库找到你想要的图标
2. 点击下载`svg`格式
3. 将下载好的`svg`文件放入 `src/assets/icons/svg`目录下
4. 在选择菜单图标时，选择你添加的图标即可

如果菜单配置里填写的是自定义图标名称，前端最终也是通过 `svg-icon` 渲染。
