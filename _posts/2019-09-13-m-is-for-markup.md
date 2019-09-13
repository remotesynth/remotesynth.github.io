---
layout: post
title: Markdown is Markup and Other Confusions Around JAMStack
date: '2019-09-13'
description: What makes a site JAMStack? A lot of it is in the M for markup.
categories:
  - web development
  - JAMStack
  - static sites
comments: true
---

Multiple times from multiple people I've heard the M in [JAMStack](https://jamstack.org/) described as standing for [Markdown](https://daringfireball.net/projects/markdown/). It's an easy mistake to make, since static site generators have been so closely tied to Markdown for so long. [Jekyll](https://jekyllrb.com/), for instance, has supported Markdown as the default way to create content pages going back to some of its earliest versions in 2009 and almost every other major static site generator today does the same. So if you know the history of the tools that the JAMStack is based upon, it makes sense to think the M is for Markdown.

## M is for Markup

However, the M is actually for _mark**up**_. Markup is a much broader term that encompasses Markdown, which is a lightweight form of markup. There are other similar types of lightweight markup that some static site generator tools support including [AsciiDoc](http://asciidoc.org/) and [LaTeX](https://www.latex-project.org/about/). HTML is also markup (it's in the name after all - Hypertext _Markup_ Language).

But Markup in the JAMStack sense is more than just Markdown or HTML. A key part of that is combining these markup languages with templating. So, for instance, Jekyll uses [Liquid](https://shopify.github.io/liquid/), [Hugo](https://gohugo.io/) uses [Go Templating](https://golang.org/pkg/text/template/) and many others use [Handlebars](https://handlebarsjs.com/) or something similar. This is part of the magic that turns what would otherwise be static files into something that can generate an entire web site filled with content that can then be deployed as HTML, CSS and JavaScript.

## M is for More

And this is where the M in JAMStack goes beyond just the Markdown, HTML, YAML and Liquid you may use. Almost any site includes JavaScript, APIs and Markup, but not all these sites are built with JAMStack. The M includes the build process to put these together - meaning the M includes your static site generator. If this is a little bit hidden in the name, that's not entirely unintended. To understand why, you need to look a little bit at the history of this approach to web development.

JAMStack was a term essentially created by [Netlify](https://www.netlify.com/) in conjunction with some other companies beginning to work on the tooling for this approach back [around 2016](https://web.archive.org/web/20160603092304/http://jamstack.org/). Having written books and articles and presented on the topic extensively, I was approached about it back then and, to be honest, I didn't love the name at the time, but I understood the reasoning behind it and, truthfully, didn't have any better suggestions.

The problem was that up until then we'd been simply calling them static sites and they were built with static site generators. This didn't reflect the reality, which was that these sites had become increasingly dynamic. Today's JAMStack sites are often indistinguishable from any other dynamic web application incorporating things like dynamic content, authentication, and much more. Calling them static sites would be both unfair and misleading. So JA**M**Stack it is - but let's emphasize the M!