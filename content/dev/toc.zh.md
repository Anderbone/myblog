+++ 
date = "2020-05-22"
title = "Hugo 添加目錄"
tags = ["hugo", "css"]
toc = true
+++

我在用這個Bootstarp的插件[TOC plugin](https://afeld.github.io/bootstrap-toc/)。添加如下的幾個css/js，最關鍵的是最後html的layout，我自己調了個能看的，大家可以參考。

## Usage
1. Set up Bootstrap v4.
    For Bootstrap v3, see the older instructions.
2. Include the Bootstrap Table of Contents stylesheet and JavaScript file.
```html
<!-- add after bootstrap.min.css -->
<link
rel="stylesheet"
href="https://cdn.rawgit.com/afeld/bootstrap-toc/v1.0.1/dist/bootstrap-toc.min.css"
/>
<!-- add after bootstrap.min.js -->
<script src="https://cdn.rawgit.com/afeld/bootstrap-toc/v1.0.1/dist/bootstrap-toc.min.js"></script>
```
3. Add this css to your customer.css. Pick one of the two options below.
```css
nav[data-toggle="toc"] {
  top: 42px;
}

/* small screens */
@media (max-width: 768px) {
  /* override stickyness so that the navigation does not follow scrolling */
  nav[data-toggle="toc"] {
    margin-bottom: 42px;
    position: static;
  }

  /* PICK ONE */
  /* don't expand nested items, which pushes down the rest of the page when navigating */
  nav[data-toggle="toc"] .nav .active .nav {
    display: none;
  }
  /* alternatively, if you *do* want the second-level navigation to be shown (as seen on this page on mobile), use this */
  /*
  nav[data-toggle='toc'] .nav .nav {
    display: block;
  }
  */
}

```
4. Determine the layout. This is my example:
```html
<body data-spy="scroll" data-target="#toc">
<div class="container-fluid">
  <div class="row">

    <div class="col-sm-2">

      {{ if or (gt .WordCount 400 ) (.Params.toc) }}
      <nav class="sticky-top" data-toggle="toc" id="toc"></nav>
      {{ end }}
    </div>

    <div class="col-sm-8">
      <section class="container post">

        <article>

          <header>
            <div class="post-title">
              <h1 class="title">{{ .Title }}</h1>
            </div>
            <div class="post-meta">
              <div class="date">
            <span class="posted-on">
              <i class="fas fa-calendar"></i>
              <time datetime='{{ .Date.Format "2006-01-02T15:04:05Z07:00" }}'>
                {{ .Date.Format (.Site.Params.dateFormat | default "January 2, 2006" ) }}
              </time>
            </span>

              </div>
              {{ with .Page.Params.Categories }}{{ partial "taxonomy/categories.html" . }}{{ end }}
              {{ with .Page.Params.Tags }}{{ partial "taxonomy/tags.html" . }}{{ end }}
            </div>
          </header>

          {{ .Content }}

          <footer>
            {{ partial "posts/series.html" . }}
            {{ partial "posts/disqus.html" . }}
            {{ partial "posts/commento.html" . }}
            {{ partial "posts/utteranc.html" . }}
          </footer>
        </article>

        {{ partial "posts/math.html" . }}

      </section>
    </div>
  </div>
</div>
</body>

```