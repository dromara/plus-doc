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
   * 使用 `@vueup/vue-quill` 实现，支持多种富文本编辑功能，如加粗、斜体、下划线、删除线、引用、代码块、有序/无序列表、缩进、字体大小、标题、字体颜色、背景颜色、对齐方式、清除格式、链接、图片、视频等。
   
     
   
2. **图片上传**：
   
   * 支持两种图片上传方式：`url` 和 `base64`。
   
   * 使用 `el-upload` 组件进行图片上传，上传前会校验文件类型和大小。
   
   * 上传成功后，将图片插入到编辑器中。
   
     
   
3. **样式调整**：
   * 通过 `styles` 计算属性动态设置编辑器的高度和最小高度。
   
   * 自定义了一些 `Quill` 编辑器的样式，以适应项目需求。
   
     

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

<script setup lang="ts">import { ref } from 'vue';
import Editor from '@/components/Editor/index.vue';

const editorContent = ref('<p>初始内容</p>');
</script>
```

### 文件上传组件

#### 参数说明

| 属性名     | 类型                    | 默认值                              | 说明                                                         |
| ---------- | ----------------------- | ----------------------------------- | ------------------------------------------------------------ |
| modelValue | `string\|object\|array` | []                                  | 上传文件的列表，支持双向绑定。可以是字符串（逗号分隔的 OSS ID）、对象或数组。 |
| limit      | `number`                | 5                                   | 允许上传的最大文件数量。                                     |
| fileSize   | `number`                | 5                                   | 上传文件的最大大小（单位：MB）。                             |
| fileType   | `array`                 | ['doc', 'xls', 'ppt', 'txt', 'pdf'] | 允许上传的文件类型，例如 `['pdf', 'doc', 'docx']`。          |
| isShowTip  | `boolean`               | true                                | 是否显示上传提示信息。                                       |

#### 事件

| 事件名            | 类型         | 说明                                         |
| ----------------- | ------------ | -------------------------------------------- |
| update:modelValue | `Function()` | 当文件列表发生变化时触发，传递新的文件列表。 |

#### 功能说明

1. **文件上传**:
   - 使用 `el-upload` 组件实现文件上传功能。
   - 支持多文件上传。
   - 上传前会校验文件类型和大小。
   - 上传成功后，将文件信息添加到文件列表中。

2. **文件列表**:
   - 显示已上传的文件列表。
   - 每个文件项包含文件名和删除按钮。
   - 点击文件名可以预览文件。

3. **上传提示**:
   - 根据 `isShowTip` 属性决定是否显示上传提示信息。
   - 提示信息包括文件大小限制和文件类型限制。

4. **文件删除**:
   - 点击删除按钮可以删除文件，并从文件列表中移除。
   - 同时调用删除文件的 API。

5. **上传状态管理**:
   - 上传过程中显示加载提示。
   - 上传成功或失败后关闭加载提示。

#### 示例代码

```vue
<template>
  <div>
    <file-upload
      v-model="fileList"
      :limit="3"
      :file-size="5"
      :file-type="['pdf', 'doc', 'docx']"
      :is-show-tip="true"
    />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import FileUpload from '@/components/FileUpload/index.vue';

const fileList = ref([
  { name: 'example.pdf', url: 'https://example.com/example.pdf', ossId: '12345' }
]);
</script>
```
