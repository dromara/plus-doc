# 内容复制
- - -

复制功能由指令 `v-copyText` 提供，源码位于 `src/directive/common/copyText.ts`。

## 基础用法

```html
<el-button v-copyText="content">复制</el-button>
```

```typescript
const content = ref('需要复制的内容');
```

## 复制回调

```html
<el-button v-copyText="content" v-copyText:callback="handleCopy">
  复制
</el-button>
```

```typescript
import modal from '@/plugins/modal';

const content = ref('需要复制的内容');

const handleCopy = (text: string) => {
  modal.msgSuccess('复制成功');
  console.log(text);
};
```

说明：

- `v-copyText` 绑定要复制的字符串
- `v-copyText:callback` 为可选回调，复制后回传当前文本
- 指令内部使用 `document.execCommand('copy')`
- 指令本身不弹出成功提示，需要在回调中自行提示

复杂对象请先转换成字符串再传入。
