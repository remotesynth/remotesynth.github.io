---
layout: post
title: "GitHub Pages Now Support HTTPS - Use It!"
date: "2018-05-01"
categories:
    - general
description: GitHub has finally announced HTTPS support.
comments: true
---

Today [GitHub announced](https://blog.github.com/2018-05-01-github-pages-custom-domains-https/) that custom domains will support HTTPS. This is great news!

As many of you may already know, [GitHub Pages](https://pages.github.com/) was a great (and completely free) way to host static sites. It has built in integration for anyone using [Jekyll](https://jekyllrb.com/) so that it will automatically rebuild your site whenever new code is checked in. However, you could deploy and host any static site, which made it a great solution for things like personal blogs or event sites or project sites.

The drawback, up until now, was that you could not use HTTPS without the support of something like [CloudFlare](https://www.cloudflare.com/), which offers a free account with a shared SSL cert. This is fine for many projects, but not always suitable. For instance, I hosted some event sites for work on GitHub pages, and you had no way to know with whom you shared the SSL cert (which, for a company, could lead to some embarrassment).

The only other option was to accept the the dreaded "Your connection to this site is not secure" warning. This warning only gets worse if, as [planned for July in Chrome 68](https://techcrunch.com/2018/02/08/chrome-will-soon-mark-all-unencrypted-pages-as-not-secure/), Chrome begins marking pages as "not secure" prominently in the address bar.

Even better, GitHub has added the ability to configure your URL to enforce HTTPS, meaning that any visitors to the unsecured version of your domain will be automatically redirected to HTTPS.

If you want to get started configuring your domain for GitHub Pages, [check the documentation](https://help.github.com/articles/using-a-custom-domain-with-github-pages/) and then walk through the instructions in the [announcement post](https://blog.github.com/2018-05-01-github-pages-custom-domains-https/) to configure SSL or in their [documentation of the feature](https://help.github.com/articles/securing-your-github-pages-site-with-https/).