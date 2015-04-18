# book.json

gitbook 在編譯書籍的時候會讀取書籍源碼頂層目錄中的 `book.js` 或者 `book.json`，這裡以 `book.json` 為例，參考 [gitbook 文檔](https://github.com/GitbookIO/gitbook) 可以知道，`book.json` 支持如下配置：

```json
{
    // Folders to use for output
    // Caution: it overrides the value from the command line
    // It's not advised this option in the book.json
    "output": null,

    // Generator to use for building
    // Caution: it overrides the value from the command line
    // It's not advised this option in the book.json
    "generator": "site",

    // Book metadats (somes are extracted from the README by default)
    "title": null,
    "description": null,
    "isbn": null,

    // For ebook format, the extension to use for generation (default is detected from output extension)
    // "epub", "pdf", "mobi"
    // Caution: it overrides the value from the command line
    // It's not advised this option in the book.json
    "extension": null,

    // Plugins list, can contain "-name" for removing default plugins
    "plugins": [],

    // Global configuration for plugins
    "pluginsConfig": {
        "fontSettings": {
            "theme": "sepia", "night" or "white",
            "family": "serif" or "sans",
            "size": 1 to 4
        }
    },

    // Variables for templating
    "variables": {},

    // Links in template (null: default, false: remove, string: new value)
    "links": {
        // Custom links at top of sidebar
        "sidebar": {
            "Custom link name": "https://customlink.com"
        },

        // Sharing links
        "sharing": {
            "google": null,
            "facebook": null,
            "twitter": null,
            "weibo": null,
            "all": null
        }
    },


    // Options for PDF generation
    "pdf": {
        // Add page numbers to the bottom of every page
        "pageNumbers": false,

        // Font size for the fiel content
        "fontSize": 12,

        // Paper size for the pdf
        // Choices are [u’a0’, u’a1’, u’a2’, u’a3’, u’a4’, u’a5’, u’a6’, u’b0’, u’b1’, u’b2’, u’b3’, u’b4’, u’b5’, u’b6’, u’legal’, u’letter’]
        "paperSize": "a4",

        // Margin (in pts)
        // Note: 72 pts equals 1 inch
        "margin": {
            "right": 62,
            "left": 62,
            "top": 36,
            "bottom": 36
        },

        //Header HTML template. Available variables: _PAGENUM_, _TITLE_, _AUTHOR_ and _SECTION_.
        "headerTemplate": null,

        //Footer HTML template. Available variables: _PAGENUM_, _TITLE_, _AUTHOR_ and _SECTION_.
        "footerTemplate": null
    }
}
```

注意：上面的內容直接從 [gitbook 文檔](https://github.com/GitbookIO/gitbook) 中複製，所以可能過期！

首先，將這個文件放到書籍代碼頂層目錄中，命名為 `book.json`，然後編譯書籍：

```bash
$ gitbook build
```

可以看到，編譯完成，使用

```bash
$ gitbook serve
```

然後將瀏覽器指向 `http://127.0.0.1:4000`，可以看到，什麼都沒有改變！

是的，雖然這裡 `book.json` 文件非法，但是 `gitbook build` 並沒有報錯！所以，用戶需要自己準備工具來保證 `book.json` 必須是一個合法的 JSON 文件，並且不能含有非法配置項。

首先，刪除註釋項，以及空行，如果是在 vim 中，可以執行下面的命令：

```vim
:%g/\s*\/\//d
:%g/^\s*$/d
```

然後，使用 python 來檢查 book.json 是否合法，同樣，在 vim 中執行下面的命令：

```vim
:%!python -m json.tool
```

很顯然，下面的配置不能通過，所以刪去（注：但是默認主題卻是使用的這個配置！）。

```json
    "pluginsConfig": {
        "fontSettings": {
            "theme": "sepia", "night" or "white",
            "family": "serif" or "sans",
            "size": 1 to 4
        }
    },
```

最後，剩下的內容如下：

```json
{
    "description": null,
    "extension": null,
    "generator": "site",
    "isbn": null,
    "links": {
        "sharing": {
            "all": null,
            "facebook": null,
            "google": null,
            "twitter": null,
            "weibo": null
        },
        "sidebar": {}
    },
    "output": null,
    "pdf": {
        "fontSize": 12,
        "footerTemplate": null,
        "headerTemplate": null,
        "margin": {
            "bottom": 36,
            "left": 62,
            "right": 62,
            "top": 36
        },
        "pageNumbers": false,
        "paperSize": "a4"
    },
    "plugins": [],
    "title": null,
    "variables": {}
}
```

現在，修改一些配置，修改後為：

```json
{
    "author": "Chengwei Yang <me@chengweiyang.cn>",
    "description": "This is a sample book created by gitbook",
    "extension": null,
    "generator": "site",
    "isbn": null,
    "links": {
        "sharing": {
            "all": null,
            "facebook": null,
            "google": null,
            "twitter": null,
            "weibo": null
        },
        "sidebar": {
            "Chengwei's Blog": "http://www.chengweiyang.cn"
        }
    },
    "output": null,
    "pdf": {
        "fontSize": 12,
        "footerTemplate": null,
        "headerTemplate": null,
        "margin": {
            "bottom": 36,
            "left": 62,
            "right": 62,
            "top": 36
        },
        "pageNumbers": false,
        "paperSize": "a4"
    },
    "plugins": [],
    "title": "Sample GitBook",
    "variables": {}
}
```

現在，重新編譯書籍，預覽效果，如下圖所示：

![configure book.json](../assets/customize/book-json.png)

可以看到，書籍的標題變成了 "Sample GitBook"，而且在左邊的導航欄中添加了一個鏈接！

需要注意的是：GitBook.com 上的書籍標題經試驗不能通過配置 `book.json` 的方式修改 `title`，需要在書籍的屬性頁面中的 'Settings' 中進行修改！
