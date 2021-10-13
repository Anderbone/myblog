+++ 
date = "2021-02-22"
title = "Hugo: How to add last update"
tags = ["tool", "dynalist", "hugo"]
+++
Under layouts/posts/single.html, check if the day publish is the same day we update, don't show the last udpated.

```html
<div class="date">
    <span class="posted-on">
    <i class="fas fa-calendar"></i>
    <time datetime='{{ .Date.Format "2006-01-02T15:04:05Z07:00" }}'>
        {{ .Date.Format (.Site.Params.dateFormat | default "January 2, 2006" ) }}
    </time>
    </span>

    {{ if ne .Date.YearDay .Lastmod.YearDay }}
    <span class="post-on">
    <i class="fas fa-calendar"></i>
    <time datetime='{{ .Date.Format "2006-01-02T15:04:05Z07:00" }}'>
        Last updated:
        {{ dateFormat ( or $.Site.Params.dateFormat "2006, Jan 02" ) $.Page.Params.LastMod }}
    </time>
    </span>
    {{ end }}

</div>
```