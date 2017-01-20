---
layout: post
title: "Rising Stars for Static Site Generators in 2016"
date: "2017-01-17"
categories:
    - static sites
description: Probably not who you're expecting.
comments: true
---

[Best.of.js](http://bestof.js.org/) published its list of [rising stars for 2016](https://risingstars2016.js.org/). This list uses the number of GitHub stars added on a project over the course of the year to determine which projects are trending the most for the year. This may be an imperfect measure, to be sure, but it is at least illustrative of interest on some level in a project.

So who were the [rising stars for static site generators](https://risingstars2016.js.org/#ssg)? Probably not who you'd expect.

![Rising static site generators](/images/posts/rising_ssg_2016.png)

Interestingly, for a type of tool where we seem to see a new project almost daily, the majority of these are not new. Hexo, Metalsmith and Harp have all been around for quite some time now. Harp was the most surprising to me since it first appeared in 2012 and hasn't seen a meaningful update in years (it still works as advertised though, in my experience). Gatsby and Phenomic are relatively new (both appearing in 2015) but their appearance is less surprising since they both are based upon the React framework which was what all the cool kids used in 2016 (though, they've since moved on to Vue apparently).

This is also a measure of the fact that users seem to want tools written in the language they use - in this case, JavaScript. Every one of these tools in written in JavaScript (as you would expect from Best of JS). I've personally used Hexo, Metalsmith and Harp (they are part of my [static site samples](https://github.com/remotesynth/Static-Site-Samples)). I hate to offend anyone, but, based upon my personal experience, if you value using the best tool for the job over the language (or framework) that it is written in, these would not be the tools that I'd most recommend. I recommend [Jekyll](http://jekyllrb.com/) (built with Ruby) or [Hugo](http://gohugo.io/) (built with Go).

If you _insisted_ on using a JavaScript-based tool, Hexo is certainly a worthwhile choice. But I would ask, why are you insisting? Certainly, there are legitimate reasons. For example, there is very specific custom functionality that you require and intend to add via an extension of some sort (and which isn't supported by any existing extensions for the tools I suggest). However, these exceptions are rare.

Obviously, I haven't used every tool on this list (or the literally [445 others](https://staticsitegenerators.net/) that exist as of today), but I have used more than most. I'm always willing to give a new tool a shot. It can be fun. But if I am starting a legitimate project, I'd stick with the best available and most established tools for the job.