+++ 
date = "2020-05-22"
title = "Hugo website optimization: Table of Contents"
tags = ["hugo"]
+++

This [TOC plugin](https://afeld.github.io/bootstrap-toc/) using bootstrap is very easy to use in Hugo.

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
Put it simple, just edit layouts/_default/baseof.html. Add some scripts before the end of body, and add 2 links in the beginning.
```html
<script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>
<script src="https://cdn.rawgit.com/afeld/bootstrap-toc/v1.0.1/dist/bootstrap-toc.min.js"></script>
```
```html
<link rel="preload" href="/fonts/forkawesome-webfont.woff2?v=1.2.0" as="font" type="font/woff2" crossorigin>
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
<link
rel="stylesheet"
href="https://cdn.rawgit.com/afeld/bootstrap-toc/v1.0.1/dist/bootstrap-toc.min.css"
/>
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
4. Determine the layout. Edit layouts/posts/single.html. This is my example:

```html
{{ define "title" }}
{{ .Title }} · {{ .Site.Title }}
{{ end }}
{{ define "content" }}
<body data-spy="scroll" data-target="#toc">
  <div class="container-fluid">
    <div class="row">

      <div class="col-sm-2">

        {{ if or (gt .WordCount 400 ) (.Params.toc) }}
        <nav class="sticky-top" data-toggle="toc" id="toc"></nav>
        {{ end }}
      </div>

      <div class="col-sm-8">
        section...
      </div>
    </div>
  </div>
</body>
{{ end }}

```
Full page:

```html
{{ define "title" }}
{{ .Title }} · {{ .Site.Title }}
{{ end }}
{{ define "content" }}

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
                <h1 class="title">
                  <a class="title-link" href="{{ .Permalink | safeURL }}">
                    {{ .Title }}
                  </a>
                </h1>
              </div>
              <div class="post-meta">
                <div class="date">
                  <span class="posted-on">
                    <i class="fa fa-calendar" aria-hidden="true"></i>
                    <time datetime='{{ .Date.Format "2006-01-02T15:04:05Z07:00" }}'>
                      {{ .Date.Format (.Site.Params.dateFormat | default "January 2, 2006" ) }}
                    </time>
                  </span>
                </div>
                {{ with .Page.Params.Authors }}{{ partial "taxonomy/authors.html" . }}{{ end }}
                {{ with .Page.Params.Categories }}{{ partial "taxonomy/categories.html" . }}{{ end }}
                {{ with .Page.Params.Tags }}{{ partial "taxonomy/tags.html" . }}{{ end }}
              </div>
            </header>

            <div>
              {{ if .Params.featuredImage }}
              <img src='{{ .Params.featuredImage }}' alt="Featured image" />
              {{ end }}
              {{ .Content }}
            </div>


            <footer>
              {{ partial "posts/series.html" . }}
              {{ partial "posts/disqus.html" . }}
              {{ partial "posts/commento.html" . }}
              {{ partial "posts/utterances.html" . }}
            </footer>
          </article>

          {{ partial "posts/math.html" . }}
        </section>

      </div>
    </div>
  </div>
</body>
{{ end }}
```