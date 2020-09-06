+++ 
date = "2020-05-08"
title = "Hugo優化：代碼高亮，添加Copy按鈕，數學公式"
slug = "" 
tags = ["hugo", "javascript", "css"]
categories = []
externalLink = ""
series = []
toc = true
+++

最近在Hugo上建立了個個人網站，就不從零開始講了。
參考鏈接：[零成本搭建现代博客之搭建篇](https://www.bmpi.dev/dev/guide-to-setup-blog-site-with-zero-cost-1/)。
將網站基於這位同學的建起來后，還有幾點想要修改的：
- 代碼高亮
- 代碼Copy按鈕
- 數學公式
- Google analytics
### 代碼高亮
hugo-coder主題的這個默認的代碼高亮太難看了。
其實有很多辦法，對這個主題，其實把config.toml裏面的pygments相關參數刪掉就能看了。
更多可以參考官方文檔hugo [doc](https://gohugo.io/content-management/syntax-highlighting/)。
### 代碼Copy按鈕
[Reference](https://www.dannyguo.com/blog/how-to-add-copy-to-clipboard-buttons-to-code-blocks-in-hugo/)
基於參考鏈接，更改了按鈕的顔色和位置，放到了代碼塊裏面。
```css
.copy-code-button {
    color: #c4c5c6;
    background-color: #444444;
    /*border: 2px solid;*/
    border-width: 0 0 0 0;
    /*border-left-color: rgba(32, 226, 226, 0.45);*/
    /*border-bottom-color: #20e2e2;*/
    border-radius: 4px 4px 4px 4px;
    position:relative;

    /* right-align */
    display: block;
    margin: 0 2px -32px auto;
    padding: 0 7px;
    font-size: 0.8em;
    font-family: Monoco, serif;
}

.copy-code-button:hover {
    cursor: pointer;
    background-color: #636262;
}

.copy-code-button:focus {
    /* Avoid an ugly focus outline on click in Chrome,
       but darken the button for accessibility.
       See https://stackoverflow.com/a/25298082/1481479 */
    background-color: #110a0a;
    outline: 0;
}

.copy-code-button:active {
    background-color: #241c1c;
}

.highlight pre {
    /* Avoid pushing up the copy buttons. */
    margin: 0;
}


```
### 數學公式
Put this script in layout/footer.html.
```javascript
  <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [['$','$'], ['\\(','\\)']],
            displayMath: [['$$','$$'], ['\[','\]']],
            processEscapes: true,
            processEnvironments: true,
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            TeX: {
                equationNumbers: { autoNumber: "AMS" },
                extensions: ["AMSmath.js", "AMSsymbols.js"]
            }
        }
    });
</script>
```

### Google analytics
All you need to do is to paste your own UA code in your config.toml.
```css
googleAnalytics = "UA-16xxx-1"
```