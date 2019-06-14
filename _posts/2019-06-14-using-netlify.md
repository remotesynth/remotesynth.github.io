---
layout: post
title: Using Netlify to the Fullest
date: '2019-06-14'
description: Finally taking advantage of some of the platform's more advanced features.
categories:
  - static sites
  - web development
comments: true
---

Some tools make getting started so simple that it becomes easy to overlook all the features it offers. When everything "just works" out of the box, there's nothing necessarily pushing you to dig deeper. Take, for example, [Netlify](https://www.netlify.com/).

I've been using them for years now, most importantly for my online meetups and training site called [Certified Fresh Events](https://cfe.dev/). The original site launched about two years ago was built with [Hugo](https://gohugo.io/) (the newly launched version is also built with Hugo). Building the site took some time and effort, deploying it to Netlify took all of 5 minutes. However, outside of a limited use of their [form handling](https://www.netlify.com/docs/form-handling/), I really wasn't using any Netlify features other than continuous deployment.

However, with the recent re-launch of the site built from the ground up, I have finally started to use some of the real power of Netlify. In this post, I want to discuss some of those features.

> NOTE: Yes, I am gushing a bit about Netlify, so it is worth noting that I do not work for them, have not been asked to write this, nor am I being compensated in any way for this post. This is a service that I legitimately love because it has enabled me to run my events site, blog and more for years.

## Environment Variables

Honestly, this is a simple one, but since I wasn't doing anything fancy before the only environment variable I had set was my Hugo version. [Environment variables](https://www.netlify.com/docs/continuous-deployment/#environment-variables) are a good place to keep things like API keys that you don't want to include in your repository.

There are two ways to define environment variables, one is via the `netlify.toml` file in your project. This is useful if you are using environment variables for something other than an API key however, since it will be checked in with your repository. The other way is to set them in the UI. You can set site specific environment variables by going to Settings > Build & Deploy > Environment.

![Environment variables](/images/posts/netlify/environment_variables.png)

## Branch Deploys

Netlify gives you a lot of options for [previewing potential changes to your site](https://www.netlify.com/docs/continuous-deployment/#branches-deploys), from allowing you to view a pull request or merge request to previewing a branch. This is a feature I had turned on since day one but never taken advantage of. In this case, though, I was doing a significant redesign of my site and working via a branch was the obvious direction.

Deploy previews for pull requests and branch deploys are turned on by default, but you can find the settings under Settings > Build & Deploy > Continuous Deployment > Deploy Contexts.

![Branch Deploys](/images/posts/netlify/deploy_contexts.png)

What does this mean? Well, in my case, my branch was called "redesign" so my branch was automatically deployed to `redesign.cfe.dev` based on my primary domain name. This not only allowed me to preview my work but even to share it publicly to test the redesign before I officially launched it for everyone.

## Netlify Functions

The key difference between [JAMstack](https://jamstack.org/) and static sites is that JAMstack has static assets but the site itself can be dynamic by leveraging JavaScript and APIs. A key piece of this, from a Netlify perspective, are [functions](https://www.netlify.com/docs/functions/). Functions, which are built on AWS, essentially allow me to build chunks of server side code that allow my "static site" to do things a traditional static site is incapable of.

I will admit to feeling some pain when getting started with functions. Part of this was that the tutorials I found relied upon the [netlify-lambda](https://github.com/netlify/netlify-lambda) tool for developing functions. This works but was a bit more complicated as it involved a build process whereas the newer method for developing functions using [Netlify Dev](https://www.netlify.com/products/dev/) is much more streamlined. (Just to note that Netlify Dev does a heck of a lot more than just functions.)

I won't go into great detail on what I did, largely because my good friend Raymond Camden [already covered it](https://www.netlify.com/products/dev/). We had taken different approaches to this problem and, as it turned out, his was better. I made some adjustments to suit my use case, but the core stayed the same - it is a simple function that allowed me to subscribe people to Mailchimp without leaving my site. While this is a limited use of functions, it is definitely a feature that I plan to leverage more as I continue to develop this site.

## Scheduling Deploys

The last feature that I want to discuss isn't really a built-in feature of Netlify per se. As my content is very date sensitive, I wanted to have the site continuously rebuilt so that the date information doesn't become stale (for example, an upcoming event may have text that says "in 12 days"). In addition, I have random items displayed in some spots on the home page, which also requires a rebuild since the random items are chosen at build time. So what I needed was to ensure that the site regularly rebuilds itself without requiring my direct intervention.

Luckily, Netlify has pre-built integration with [Zapier](https://zapier.com). Zapier isn't free, but, for this sort of task, you're unlikely to hit their free account limits. It's a very simple two-step "Zap" that uses Zapier's Schedule to trigger a deploy every night at midnight (truthfully, the time doesn't matter that much from a Netlify standpoint since the build occurs in the background, but midnight made sense since the dates would change, thereby changing the date math).

![Zapier](/images/posts/netlify/zapier.png)

## Just Getting Started

A more honest title for this post would have been "Using Netlify to the Fuller", but, on top of being grammatically incorrect, it isn't quite as catchy. It would be more accurate though in the sense that there are still a ton of features that I am not fully taking advantage of - things like split testing, identity, large media. But I have finally explored beyond just the simplicity of the build and deploy process and am excited to continue learning.