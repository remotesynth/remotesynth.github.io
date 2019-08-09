---
layout: post
title: Knowing the Web's History is Critical to Its Present and Future
date: '2019-08-09'
description: Understanding the history of the web will help guide you to its future. 
categories:
  - general
  - web development
comments: true
---

I've always believed in the importance of understanding history. In college, I was not a Computer Science major, but a history major. History is about much more than understanding the past, it explains where we are today, without which we cannot know where we are going. Imagine you suddenly wake up with no memory of anything prior. You are told that the only safe path is to continue forward, but what is forward if you don't know where you've been?

In technology and development, we focus on the idea of progress. The web platform of today, for instance, is better than the web platform of a few years ago and far better than the web platform of 20 years ago. Defining progress requires an understanding the historical context.

## But Why Does History Matter for Front-End Development?

History is uniquely important to the web because the web is a platform where we've committed to essentially full backwards compatibility. This backwards compatibility can sometimes extend beyond the platform itself to even the tools developers use to build on it. Let's take a relatively recent example.

Remember "smooshgate"? This was the controversy that grew over the suggestion of slightly ridiculous sounding method name suggestion of `Array.smoosh()` to flatten an array. Why was this even an issue? Well, because way back when there was a tool called MooTools that was quite popular, and it used JavaScript's prototypal inheritance to extend an array with the `flatten()` method. Thus, adding `Array.flatten()` would have broken any existing site that still ran on MooTools. Jay Hoffman, author of the excellent [History of the Web newsletter](https://thehistoryoftheweb.com/) has a [great, in depth overview](https://css-tricks.com/yet-another-javascript-framework/) of this.

Another example revolves around Flash and its impact on the development not just of HTML5 but of many of the tools and frameworks that followed its slow demise. As I talked about in [What the Web Owes Flash](https://dev.to/remotesynth/what-the-web-owes-flash), the web platform spent some time playing catch up to the capabilities of Flash. For example, the 3D visualizations and games that are now possible on the web through things like WebGL and [GLSL shaders](https://developer.mozilla.org/en-US/docs/Games/Techniques/3D_on_the_web/GLSL_Shaders) were possible 8 years ago in Flash using Stage3D. What was done in Flash has greatly influenced how the web platform has evolved to today.

## Understanding the History Makes You a Better Developer

Understanding the history improves the depth of your understanding of the web platform. It takes you a long way from just understanding how a feature works to why it works the way it does. Going back to my analogy at the beginning, it also orients you to what direction is forward. Understanding how we got here and why is the best guide to understanding how we can progress.

---

The importance of the history of the web is why I created [Flashback Conference](https://flashback.dev), which is dedicated to covering new features, tools and frameworks on the web platform while also understanding the history behind them.

[![Flashback Conference](/images/posts/flashback.jpg)](https://flashback.dev)

The conference will be in Orlando (my hometown) on February 10-11, 2020. I really think this will be an amazing and fun event, and I've already got some fantastic speakers and sponsors lined up and ticket are already on sale. I really hope you'll join us.

Also, if you love this topic as much as I do, I highly recommend Jay Hoffman's [History of the Web newsletter](https://thehistoryoftheweb.com/) (and Jay will also be speaking at Flashback Conference).