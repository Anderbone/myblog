+++ 
date = "2020-05-08"
title = "Hugo website optimization: Copy-code button, Math Latex, Google analytics"
slug = "" 
tags = ["hugo", "javascript", "css"]
categories = []
externalLink = ""
series = ["hugo"]
toc = true
+++

Recently I did several changes on hugo. 
### Code highlight
There are many ways to make the syntax highlight better, for this hugo-coder theme, all we need to do is delete those pygments related config in config.toml.
See the hugo [doc](https://gohugo.io/content-management/syntax-highlighting/) to find more options.
### Copy code button
[Reference](https://www.dannyguo.com/blog/how-to-add-copy-to-clipboard-buttons-to-code-blocks-in-hugo/)
I just changed the css to make the button within the code.
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
### Math formula
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
