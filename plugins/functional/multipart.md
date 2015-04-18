# multipart

[multipart](https://www.npmjs.com/package/gitbook-plugin-multipart) 插件可以將書籍分成幾個部分，例如：

- GitBook Basic
- GitBook Advanced

對有非常多章節的書籍非常有用，分成兩部分後，各個部分的章節都從 1 開始編號。

## 安裝及配置

和安裝其它插件一樣，執行以下命令：

```bash
$ npm install gitbook-plugin-multipart -g
```

然後編輯 `book.json` 添加 multipart 到 plugins 中：

```json
    "plugins": [
        "multipart"
    ],
```
