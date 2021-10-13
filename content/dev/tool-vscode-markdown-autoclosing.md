+++ 
date = "2020-10-24"
title = "Auto close quotes for markdown in VsCode"
tags = ["vscode","tool"]
+++

Sometimes I want to auto-close double quotes and '`' in markdown mode.

In settings we have such settings but they are not working in plain text files like makrdown.
![](https://i.imgur.com/mo59ZXA.png)

Find "language-configuration.json" under markdown-basic folder.
My path: `C:\Program Files\Microsoft VS Code\resources\app\extensions\markdown-basics\language-configuration.json`

Add what you want auto close and save it.
```json
    "autoClosingPairs": [
        {
            "open": "{",
            "close": "}"
        },
        {
            "open": "`",
            "close": "`"
        },
        {
            "open": "\"",
            "close": "\""
        },
        {
            "open": "[",
            "close": "]"
        },
        {
            "open": "(",
            "close": ")"
        },
        {
            "open": "<",
            "close": ">",
            "notIn": [
                "string"
            ]
        }
    ],
```

BTW use `Ctrl+M Ctrl+C` you could generate a code block in markdown. 