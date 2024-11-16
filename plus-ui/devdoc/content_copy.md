# 内容复制

- - -

如果要使用复制功能可以使用指令`v-copyText`，示例代码如下

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

参数说明：

| 参数                  | 说明       |
|---------------------|----------|
| v-copyText          | 需要复制的内容  |
| v-copyText:callback | 复制后的回调函数 |
