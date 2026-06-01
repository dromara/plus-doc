# 内容复制

- - -

如果要使用复制功能，可以使用指令 `v-copyText`，该指令默认在点击元素时执行复制。

```html

<el-button
        v-copyText="content"
        v-copyText:callback="handleCopy"
>复制
</el-button>
```

```typescript
const content = ref('需要复制的内容');
const handleCopy = (text) => {
    proxy?.$modal.msgSuccess('复制成功');
};
```

补充说明：
- `v-copyText` 绑定的是要复制的内容
- `v-copyText:callback` 为可选回调，复制成功后会把当前文本值回传
- 指令本身不会自动弹出成功提示，通常在回调里自行调用 `proxy?.$modal.msgSuccess(...)`

参数说明：

| 参数                  | 说明       |
|---------------------|----------|
| v-copyText          | 需要复制的内容  |
| v-copyText:callback | 复制后的回调函数 |

建议复制内容保持为字符串，复杂对象请先格式化后再传入。
