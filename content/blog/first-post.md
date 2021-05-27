---
title: "Hello World!"
date: 2021-05-26T16:05:49-04:00
draft: false
tags: ["first-post"]
categories: ["meta"]
math: true
---

## Hi :)

My name is Shreya.

This is probably going to be my personal site. We'll see.

## Goals

- Make a portfolio-over-the-years.
- Update regularly with what I've been working on.

## Attribution

This site is made using Hugo and its PaperMod theme! Legend goes that I looked at [3b1b's Manim documentation](https://3b1b.github.io/manim/) and loved its design. Obviously I have to start clicking on things to find more about this piece of code, so I came across [Pradyun's](https://pradyunsg.me/) website, and loved *this* design too. At this point I was kind of mind blown that there were really themes I thought were sleek and adaptable for use, so I zoomed over to Hugo, and a day later, here we are.

Probably my favorite thing is that there's an easy way to write math in here! Although it's not as versatile as Coffee and Sleep--you still need to use the terminal and write in files, and it's static, so you have to deploy new changes to master--I still really like it.

I did edit the Search template to include links to tag/category search, and the footer as well. I really tried to do something cool with the footer, but it didn't animate well, so here we are. It took me a while to figure out *how* to edit the template in the first place. I think it was okay to just edit the submodule. I... don't know though... so let's hope PaperMod doesn't update.

Actually, I'm getting a bit scared. I'm going to put the code here.

*themes/PaperMod/layouts/partials/footer.html*
```html
{{- if .Site.Params.attribution }}
    <div class="footer-hide-wrapper">
        <div {{- if .Site.Params.attributionAnimation }} class="footer-hide" {{- end }}>
            <span>
                &nbsp;·&nbsp; Powered by
                <a href="https://gohugo.io/" rel="noopener noreferrer" target="_blank">Hugo</a> +
                <a href="https://git.io/hugopapermod" rel="noopener" target="_blank">PaperMod</a>, with tweaks
            </span>
        </div>
    </div>
{{- end }}
```

*themes/PaperMod/assets/css/common/footer.css*
```css
/* my code */

.footer-hide-wrapper {
    display: inline-block;
    /* transition: width 1s; */
    /* overflow: hidden; */
}

.footer .footer-hide {
    display: inline-block;
    /* overflow: hidden; */
    opacity: 0;
    max-width: 0;
    height: 0;
    line-height: 20px;
    transition: none;
}

.footer:hover .footer-hide {
    content: attr("data-hover");
    max-width: 100%;
    opacity: 100%;
    transition: opacity 1s, max-width 0.5s;
}
```


*themes/PaperMod/layouts/_default/single.html*
```html
{{- if .Params.categories }}
        <ul class="entry-isdraft" style="list-style-type: none; display: inline-block;">
        {{- range ($.GetTerms "categories") }}
        <li style="display: inline-block; margin-left: 10px;"><a href="{{ .Permalink }}">{{ .LinkTitle }}</a></li>
      {{- end }}
    </ul>
{{- end }}
```

*themes/PaperMod/layouts/_default/search.html*
```html
<!-- my div -->
<div class="search-btn post-tags" style="padding: 0 0 20px 0;">
    <li>
        <a href="{{ "" | absLangURL }}/tags/">
            Search by tag
        </a>
    </li>
    <li>
        <a href="{{ "" | absLangURL }}/categories/">
            Search by category
        </a>
    </li>
</div>
```