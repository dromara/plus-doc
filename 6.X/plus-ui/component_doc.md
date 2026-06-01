# 组件文档

- - -

### 基础框架组件

[ElementPlus](https://github.com/element-plus/element-plus)

### 富文本编辑器

[quill](https://github.com/quilljs/quill)

### 富文本组件

#### 参数说明

| 参数名     | 类型      | 默认值 | 说明                                  |
| ---------- | --------- | ------ | ------------------------------------- |
| modelValue | `string`  |        | 编辑器的内容，支持双向绑定            |
| height     | `number`  | 400    | 编辑器的高度（单位：px）              |
| minHeight  | `number`  | 400    | 编辑器的最小高度（单位：px）          |
| readOnly   | `boolean` | false  | 是否只读模式                          |
| fileSize   | `number`  | 5      | 上传文件的最大大小（单位：MB）        |
| type       | `string`  | url    | 图片上传的类型，支持 `url`和 `base64` |

#### 事件

| 事件名            | 类型         | 说明                                     |
| ----------------- | ------------ | ---------------------------------------- |
| update:modelValue | `Function()` | 当编辑器内容发生变化时触发，传递新的内容 |

#### 功能说明

1. **富文本编辑器**：
   * 使用 `@vueup/vue-quill` 实现，支持多种富文本编辑功能，如加粗、斜体、下划线、删除线、引用、代码块、有序/无序列表、缩进、字体大小、标题、字体颜色、背景颜色、对齐方式、清除格式、链接、图片、视频等
   
     
   
2. **图片上传**：
   
   * 支持两种图片上传方式：`url` 和 `base64`
   
   * 使用 `el-upload` 组件进行图片上传，上传前会校验文件类型和大小
   
   * 上传成功后，将图片插入到编辑器中
   
     
   
3. **样式调整**：
   * 通过 `styles` 计算属性动态设置编辑器的高度和最小高度
   
   * 自定义了一些 `Quill` 编辑器的样式，以适应项目需求
   
     

#### 示例代码

```vue
<template>
  <div>
    <editor
      v-model="editorContent"
      :height="500"
      :min-height="300"
      :read-only="false"
      :file-size="5"
      :type="'url'"
    />
  </div>
</template>

<script setup lang="ts">
const editorContent = ref('<p>初始内容</p>');
</script>
```

### 文件上传组件

#### 参数说明

| 参数名     | 类型                    | 默认值                              | 说明                                                         |
| ---------- | ----------------------- | ----------------------------------- | ------------------------------------------------------------ |
| modelValue | `string\|object\|array` | []                                  | 上传文件的列表，支持双向绑定。可以是字符串（逗号分隔的 OSS ID）、对象或数组 |
| limit      | `number`                | 5                                   | 允许上传的最大文件数量                                       |
| fileSize   | `number`                | 5                                   | 上传文件的最大大小（单位：MB）                               |
| fileType   | `array`                 | ['doc', 'xls', 'ppt', 'txt', 'pdf'] | 允许上传的文件类型，例如 `['pdf', 'doc', 'docx']`            |
| isShowTip  | `boolean`               | true                                | 是否显示上传提示信息                                         |

#### 事件

| 事件名            | 类型         | 说明                                       |
| ----------------- | ------------ | ------------------------------------------ |
| update:modelValue | `Function()` | 当文件列表发生变化时触发，传递新的文件列表 |

#### 功能说明

1. **文件上传**:
   - 使用 `el-upload` 组件实现文件上传功能
   - 支持多文件上传
   - 上传前会校验文件类型和大小
   - 上传成功后，将文件信息添加到文件列表中

2. **文件列表**:
   - 显示已上传的文件列表
   - 每个文件项包含文件名和删除按钮
   - 点击文件名可以预览文件

3. **上传提示**:
   - 根据 `isShowTip` 属性决定是否显示上传提示信息
   - 提示信息包括文件大小限制和文件类型限制

4. **文件删除**:
   - 点击删除按钮可以删除文件，并从文件列表中移除
   - 同时调用删除文件的 API

5. **上传状态管理**:
   - 上传过程中显示加载提示
   - 上传成功或失败后关闭加载提示

#### 示例代码

```vue
<template>
  <div>
    <fileUpload
      v-model="fileList"
      :limit="3"
      :file-size="5"
      :file-type="['pdf', 'doc', 'docx']"
      :is-show-tip="true"
    />
  </div>
</template>

<script setup lang="ts">
const fileList = ref([]);
</script>
```

### 图片展示组件

#### 参数说明

| 参数名 | 类型              | 默认值 | 说明                                                        |
| ------ | ----------------- | ------ | ----------------------------------------------------------- |
| src    | `string`          |        | 图片的 URL，支持多个图片 URL 以逗号分隔                     |
| width  | `Number\|string` |        | 图片的宽度。可以是数字或带单位的字符串（如 `300`或`300px`） |
| height | `Number\|string` |        | 图片的高度。可以是数字或带单位的字符串（如 `200`或`200px`） |

#### 功能说明

1. 图片源处理：
   * realSrc：从 `src` 中提取第一个图片 URL 作为实际显示的图片源
   * realSrcList：从 `src` 中提取所有图片 URL 作为预览列表
   
2. 尺寸处理：
   * realWidth：根据 `width` 的类型（数字或字符串）生成实际的宽度样式
   * realHeight：根据 `height` 的类型（数字或字符串）生成实际的高度样式
   
3. 错误处理：
   * 当图片加载失败时，显示一个`ElementPlus`中的一个图标 
   
   * ```html
     <el-icon>
         <picture-filled />
     </el-icon>
     ```
   
4. 样式：
   * 图片容器设置了圆角、背景色和阴影效果
   * 鼠标悬停时，图片会放大显示
   * 加载失败时，显示居中的默认图标
   
5. 注意事项
   * 多图预览：当 `src` 包含多个图片 URL 时，点击图片会触发预览模式，显示所有图片
   * 尺寸单位：`width` 和 `height` 支持多种单位（如 px、%、em 等），也可以直接传入数字，默认单位为 px
   * 加载失败：图片加载失败时会显示一个默认图标，确保用户体验

#### 示例代码
```vue
<template>
  <div>
    <image-preview :src="imageUrl" width="300" height="200" />
  </div>
</template>

<script setup lang="ts">
const imageUrl = 'https://example.com/image1.jpg,https://example.com/image2.jpg';
</script>
```

### 图片上传组件

```vue
<template>
  <el-form>
    <el-form-item label="上传图片">
      <ImageUpload
        v-model="form.imageIds"
        :limit="5"
        :file-size="5"
        :file-type="['png', 'jpg']"
        :is-show-tip="true"
        :compress-support="true"
        :compress-target-size="300"
      />
    </el-form-item>
  </el-form>
</template>

<script setup lang="ts">

const form = reactive({
  imageIds: [] // 初始值为空数组
});
</script>
```



#### 参数说明

| 参数               | 类型                        | 默认值                 | 描述                                                         |
| ------------------ | --------------------------- | ---------------------- | ------------------------------------------------------------ |
| modelValue         | `String \| Object \| Array` | []                     | 绑定的值，可以是字符串、对象或数组。如果是字符串或对象，会自动转换为数组 |
| limit              | `Number`                    | 5                      | 允许上传的最大图片数量                                       |
| fileSize           | `Number`                    | 5                      | 单个文件的最大大小（单位：MB）                               |
| fileType           | `Array<String>`             | ['png', 'jpg', 'jpeg'] | 允许上传的文件类型                                           |
| isShowTip          | `Boolean`                   | true                   | 是否显示上传提示                                             |
| compressSupport    | `Boolean`                   | false                  | 是否支持图片压缩                                             |
| compressTargetSize | `Number`                    | 300                    | 压缩目标大小（单位：KB）。默认情况下，300KB以上的图片会被压缩至300KB以内 |

#### 事件

| 事件              | 类型         | 描述                                     |
| ----------------- | ------------ | ---------------------------------------- |
| update:modelValue | `Function()` | 当上传或删除图片时触发，传递新的图片列表 |


#### 功能说明

1. 图片上传

   * 多文件上传：支持一次选择多个文件进行上传

   * 上传地址：通过 :action="uploadImgUrl" 指定上传的服务器地址

   * 文件列表：通过 :file-list="fileList" 显示已上传的文件列表

   * 上传前检查：通过 :before-upload="handleBeforeUpload" 进行文件类型和大小的验证

   * 上传成功回调：通过 :on-success="handleUploadSuccess" 处理上传成功的响应

   * 上传失败回调：通过 :on-error="handleUploadError" 处理上传失败的情况

     

2. 文件限制

   * 文件数量限制：通过 :limit="limit" 设置允许上传的最大文件数量

   * 文件大小限制：通过 :file-size="fileSize" 设置单个文件的最大大小（单位：MB）

   * 文件类型限制：通过 :file-type="fileType" 设置允许上传的文件类型，例如 ['png', 'jpg', 'jpeg']

     

3. 上传提示

   * 显示提示：通过 v-if="showTip" 控制是否显示上传提示

   * 提示内容：根据 fileSize 和 fileType 动态生成提示内容，例如“请上传大小不超过5MB，格式为png/jpg/jpeg的文件”

     

4. 文件预览

   * 预览对话框：通过 <el-dialog> 组件实现文件预览功能

   * 预览图片：点击文件列表中的图片时，调用 handlePictureCardPreview 方法显示预览对话框

     

5. 文件删除

   * 删除确认：通过 :before-remove="handleDelete" 在删除文件前进行确认

   * 删除操作：调用 delOss 方法删除文件，并从 fileList 中移除对应的文件项

     

6. 文件压缩

   * 压缩支持：通过 :compress-support="compressSupport" 开启或关闭图片压缩功能

   * 压缩目标大小：通过 :compress-target-size="compressTargetSize" 设置压缩的目标大小（单位：KB）

   * 压缩处理：在 handleBeforeUpload 方法中，如果文件大小超过指定的压缩目标大小，则调用 compressAccurately 方法进行压缩

     

7. 数据绑定

   * 双向绑定：通过 v-model 实现数据的双向绑定，当上传或删除图片时，自动更新绑定的值

   * 初始值：通过 modelValue 接收初始值，可以是字符串、对象或数组

     

8. 加载提示

   * 上传加载：在 handleBeforeUpload 方法中显示加载提示，上传完成后关闭加载提示

   * 错误提示：在 handleUploadError 和 handleExceed 方法中显示错误提示

     

9. 样式控制

   * 隐藏上传按钮：当已上传的文件数量达到上限时，通过 :class="{ hide: fileList.length >= limit }" 隐藏上传按钮

     

#### 使用案例

```vue
<template>
  <el-form>
    <el-form-item label="上传图片">
      <ImageUpload
        v-model="form.imageIds"
        :limit="5"
        :file-size="5"
        :file-type="['png', 'jpg']"
        :is-show-tip="true"
        :compress-support="true"
        :compress-target-size="300"
      />
    </el-form-item>
  </el-form>
</template>

<script setup lang="ts">
const form = reactive({
  imageIds: [] // 初始值为空数组
});
</script>
```

### 表格分页组件


#### 参数说明

| 参数       | 类型            | 默认值                                    | 描述                                                         |
| ---------- | --------------- | ----------------------------------------- | ------------------------------------------------------------ |
| total      | `number`        |                                           | 总条数，必填                                                 |
| page       | `number`        | 1                                         | 当前页码                                                     |
| limit      | `number`        | 20                                        | 每页显示条数                                                 |
| pageSizes  | `Array<number>` | [10, 20, 30, 50]                          | 可选的每页显示条数选项                                       |
| pagerCount | `number`        | document.body.clientWidth < 992 ? 5 : 7   | 移动端页码按钮的数量，默认值为5，PC端为7                     |
| layout     | `string`        | 'total, sizes, prev, pager, next, jumper' | 分页组件的布局，可用值有`total`, `sizes`, `prev`, `pager`, `next`, `jumper` |
| background | `boolean`       | true                                      | 是否显示背景色                                               |
| autoScroll | `boolean`       | true                                      | 是否自动滚动到顶部                                           |
| hidden     | `boolean`       | false                                     | 是否隐藏分页组件                                             |
| float      | `string`        | right                                     | 分页组件的对齐方式，可用值有`left`, `center`, `right`        |

#### 事件说明

| 事件           | 描述                       | 参数                      |
| -------------- | -------------------------- | ------------------------- |
| `update:page`  | 当前页码发生变化时触发     | 新的页码值                |
| `update:limit` | 每页显示条数发生变化时触发 | 新的每页显示条数值        |
| `pagination`   | 分页组件发生改变时触发     | 包含`page`和`limit`的对象 |

#### 功能说明

1. 分页显示：

   * 显示总条数、每页显示条数选择器、上一页、下一页、页码导航和跳转输入框

   * 支持自定义分页组件的布局

     

2. 响应式设计：

   * 根据屏幕宽度自动调整页码按钮的数量，移动端默认显示5个页码按钮，PC端默认显示7个页码按钮

     

3. 事件处理：

   * 处理每页显示条数变化和当前页码变化事件，触发相应的回调函数

   * 提供自动滚动到页面顶部的功能

     

4. 样式定制：

   * 支持背景色显示和隐藏分页组件
   * 支持分页组件的对齐方式（左对齐、居中对齐、右对齐）

#### 使用案例

```vue
<template>
  <div>
    <el-table :data="tableData">
      <el-table-column prop="date" label="日期" />
      <el-table-column prop="name" label="姓名" />
      <el-table-column prop="address" label="地址" />
    </el-table>
    <pagination 
       v-show="total > 0" 
       v-model:page="queryParams.pageNum" 
       v-model:limit="queryParams.pageSize" 
       :total="total" @pagination="getList" 
     />
  </div>
</template>

<script setup lang="ts">
const tableData = ref<any[]>([]);
const total = ref(0);
const queryParams: {
    pageNum: 1,
    pageSize: 10
}

const tableData = ref([]);
    
// 模拟异步请求获取数据
const getList = async () => {
  // 发送请求
  const res = await getList(queryParams.value);
  tableData.value = res.rows;
  total.value = res.total;
};

</script>
```

