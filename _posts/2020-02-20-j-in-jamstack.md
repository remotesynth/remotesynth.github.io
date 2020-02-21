---
layout: post
title: The J in JAMstack Does Not Stand for React (or Angular, Vue, Svelte, etc.)
date: '2020-02-20'
description: Correcting what seems to be a common misconceptions about what makes an app JAMstack
categories:
  - JAMstack
comments: true
---

Once upon a time, I was asked to present the best static site generators for JavaScript developers. I painstakingly went through each of the available options at the time and then got to the end where I revealed which one I recommended. The answer: none of them. Compared to the other options at the time (Jekyll, Hugo, Middleman), they were slow, less full-featured and lacking in much of an existing ecosystem (or documentation).

Thankfully, that is not the case anymore. There are a ton of great options for JavaScript developers including [Gatsby](https://www.gatsbyjs.org/), [Next.js](https://nextjs.org/) and [React Static](https://github.com/react-static/react-static) if you prefer React, [Nuxt](https://nuxtjs.org/), [Gridsome](https://gridsome.org/) and [VuePress](https://vuepress.vuejs.org/) if you prefer Vue, and more recently, [Scully](https://github.com/scullyio/scully) for those who prefer Angular.

The existence of mature JavaScript-based tools has been part of the growth of the overall usage of static site generators, which are a key ingredient in the JAMstack. However, this seems to be fueling a common misconception that the frameworks themselves are a key part of the JAMstack - that the J in JAMstack is for your JavaScript framework. This is _not_ the case.

It's important to keep in mind that in 2016 when the term JAMstack first came about, Gatsby was little more than a year into its existence and far from the powerhouse it is today. Next.js came around in 2017; Gridsome in 2018. The point is, JavaScript frameworks were not even a relevant factor in the the term JAMstack. The role of JavaScript as [originally defined](https://web.archive.org/web/20160527203229/http://jamstack.org/) was as follows:

> JavaScript is in charge of any dynamic programming during the request/response cycle and runs entirely on the client.

My goal here is not to dissuade you from using a JavaScript framework. If you are a JavaScript developer, there are great tools for you if you'd like to use a JavaScript-based static site generator. However, I think it is a mistake if we confuse the term whereby JAMstack becomes synonymous with JavaScript frameworks. I believe one of JAMstack's strengths is the variety of options that are available (though, the variety of choices can also make JAMstack a bit intimidating). The fact that there are enough tools, even among just the widely used ones, for developers with varying programming backgrounds, whether that is JavaScript, Ruby, Go, Python, or others. If you're a developer, it's likely that regardless of what you program in, there is a static site generator that fits into your JAMstack.