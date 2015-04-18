# Disqus

[Disqus](https://disqus.com) 是一個非常流行的為網站集成評論系統的工具，同樣，gitbook 也可以集成 disqus 以便可以和讀者交流。

首先，需要在 disqus 上註冊一個賬號，然後添加一個 website，這會獲得一個關鍵字，然後在集成時配置這個關鍵字即可。

## 安裝 disqus 插件

可以參考 [插件項目主頁](https://github.com/GitbookIO/plugin-disqus) 來安裝，命令如下：

```bash
$ npm install gitbook-plugin-disqus -g
```

然後，修改 `book.json` 配置文件，添加插件的配置內容：

```json
{
    "plugins": ["disqus"],
    "pluginsConfig": {
        "disqus": {
            "shortName": "introducetogitbook"
        }
    }  
}
```

注意：上面的 `shortName` 的值就是你在 disqus 上創建的 website 獲得的唯一關鍵字。

效果如下圖所示：

![disqus](../../assets/plugins/disqus.png)
