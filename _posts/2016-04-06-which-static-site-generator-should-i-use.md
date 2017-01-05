---
layout: post
title: "Which Static Site Generator Should You Choose?"
date: "2016-04-06"
categories:
    - web development
    - static sites
description: Which static site generator do I recommend? The simple answer is easy.
comments: true
---

As part of the process of writing my [Static Site Generators ebook](http://www.oreilly.com/web-platform/free/static-site-generators.csp) for O'Reilly and maintaining my [Static Site Samples project](https://github.com/remotesynth/Static-Site-Samples) on GitHub, I've used a good number of static site generators including: Jekyll, Middleman, Hugo, Wintersmith, Metalsmith, Harp, Hexo, DocPad and Roots.

You'd think 9 static site generators is a lot, but that's out of a [list of 423](https://staticsitegenerators.net/) (as of this writing anyway). Still, it includes many of the leading projects and more than any normal person would want to try before choosing one. Because of this I am often asked (and often present on) which static site generator I recommend (based upon the ones I've used).

Let me give you the simple answer first, then the more nuanced answer second.<!--more-->

## The Simple Answer

The simple answer is [Jekyll](http://jekyllrb.com/).

Why? Here are some reasons.

- Jekyll is the most mature solution out there. This means you are very unlikely to encounter quirky issues, growing pains or drastic, breaking changes.
- Jekyll has some of the best documentation of any of the options. It's not perfect (which documentation ever is?) but I've found it covers most typical use cases.
- Jekyll's community is the largest (afaik). This means that if there are questions that aren't answered in the docs, you'll likely find answers to them. And it also means that the list of available [plugins](https://jekyllrb.com/docs/plugins/) and templates for Jekyll is very large - you'll rarely find yourself having to solve a problem yourself.
- While Jekyll is built in Ruby, you probably don't even need to care. Jekyll does a good job of shielding you from ever having to dig into Ruby to solve your problems. The available functionality within Jekyll itself usually solves the problem or, if not, the array of available plugins likely will.
- Liquid is a solid templating solution. Sure, you can change from Liquid, but having used a ton of templating options for the various generators, I can tell you that Liquid offers more out-of-the-box than most (and Jekyll even enhances the built-in offerings).
- There are a growing number of tools that support Jekyll. From GitHub Pages to CloudCannon to Netlify to [Forestry.io](http://forestry.io), the list of solutions that support Jekyll is growing. Sure, many of these support other solutions, but every one supports Jekyll.

My only significant criticism of Jekyll would be its [lack of official support for Windows](https://jekyllrb.com/docs/windows/). While the [suggested workaround](http://jekyll-windows.juthilo.com/) appears to work fine (I've personally tested it on Windows 8 and 10), the fact that a workaround is required for a significant portion of potential users to install Jekyll is suboptimal, in my opinion.

There was an old saying (which may no longer be true) that "No one ever got fired for choosing IBM." When it comes to a static site generator, I'd say "No one ever got fired for choosing Jekyll." It is a great solution and by far the safest bet of the 423 options.

## The Nuanced Answer

The more nuanced answer would take into account your specific needs.

If you are building a large site, with a lot of pages, build times cane be a concern. Solutions like Netlify, for example, allow you to avoid the local build-and-push scenario that can be slow and tedious as your site grows. But if you are concerned that build times could be a major concern for you going forward, it may be worth evaluating [Hugo](http://www.gohugo.io/). Hugo (built in Go) had by far the fastest build times of any of the solutions I tried. You can't completely avoid learning Go to use it, which can increase the learning curve, but it is also very well documented.

Some people _really, really, really_ want a solution built in JavaScript (of which, there are currently 90 and counting). In fact, this was the basis of my recent presentation at the Fluent conference in San Francisco (embedded below).

<iframe width="560" height="315" src="https://www.youtube.com/embed/sMLs0o-LqQY" frameborder="0" allowfullscreen></iframe>

If you watched the whole thing, you know I actually recommend not using any of the JavaScript options that I have tried so far. But if you are determined to do so, I recommend [Wintersmith](http://wintersmith.io/). Sure, it's written in CoffeeScript (which you may hate) and it is very sparsely documented (outside of a short quick start guide), but it does have a lot of plugins and a very solid [list of example sites](https://github.com/jnordberg/wintersmith/wiki/Showcase) (many with source available) to help. Plus, though I don't advocate using a project's source as documentation, in the absence of documentation, the source of Wintersmith is pretty readable (plus, the lack of documentation plagues every JavaScript-based option I have tried). So, I'm actually not recommending you choose it, but if you are dead-set on a JavaScript option, it's the best I've tried.

## Conclusion

To sum up... Use Jekyll unless you have a specific, legitimate reason not to do so. At the very least, start your evaluation with Jekyll. If you want to evaluate several options, of the ones I've tried go with Jekyll, Hugo and [Middleman](https://middlemanapp.com/) (also built in Ruby). Obviously, there are 414 other solutions out there that I have not evaluated (and I keep trying to get to more of them), but, in reality, one of those three solutions should suit your needs, whatever they may be.