在高级修改中，修改相关配置值：

#### 自动下载器选项

`extensions.zotero.findPDFs.resolvers：`
粘贴以下部分

```
{
    "name":"Sci-Hub",
    "method":"GET",
    "url":"https://sci-hub.ren/{doi}",
    "mode":"html",
    "selector":"#pdf",
    "attribute":"src",
    "automatic":true
}
```

