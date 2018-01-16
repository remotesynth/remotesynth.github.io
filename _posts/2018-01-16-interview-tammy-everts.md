---
layout: post
title: "Why Web App Performance Matters and What to Watch Out For - An Interview with Tammy Everts"
date: "2018-01-16"
categories:
    - general
description: Tammy Everts talks about what performance metrics matter most to developers.
comments: true
---

[![
Improving Your Apps - Performance and Debugging](/images/posts/Banner_Improving-You-Apps-Debugging.jpg)](https://certifiedfreshevents.com/events/improving-your-apps/)

[Tammy Everts](https://twitter.com/tameverts) is one of the featured speakers at [Improving Your Apps - Performance and Debugging](https://certifiedfreshevents.com/events/improving-your-apps/) online event that I am running this Wednesday, January 17 at 12pm ET. You can [sign up for free today](https://certifiedfreshevents.com/events/improving-your-apps/).

I've been a fan of Tammy's for years - her writing on the topic of web performance has been important and influential for years. I then had the opportunity to see her speak at an event several years back at Web Unleashed and I remember thinking something like, "This topic is so important to developers, but these sessions are often at non-developer events." I was already involved with the Fluent conference committee, so I suggested to Tammy that she think about submitting to Fluent 2016. Of course, she was a huge hit - so much so that she became a co-chair the conference itself the following year!

The good news is that developers seem to be paying more attention to the performance of their web apps. The bad news is, it can be hard to know what metrics to pay attention to! I asked Tammy about this.

> **For those who don't already know you, tell us a little bit about yourself? How did your career lead you to focus on web performance?**

I always feel like the first thing I need to tell people is that I’m not a developer or an engineer. For a long time, that made me a bit of an oddity in the performance industry, though actually it’s been more of an advantage than anything else. My background is in studying usability and user experience, which I’ve been doing for twenty years, starting with designing and conducting usability lab studies back in the early days of the web.

About nine years ago, I started working in performance and was immediately fascinated by this brand-new (to me, anyway) dimension of UX – page speed – which had previously been ignored by most usability folks. The fact that you could measure the impact of performance on both UX metrics and business KPIs (like cart size, revenue, and user retention) was – and still is – very exciting to me. In the past few years, I’ve done a lot of original research in this area, as well as studying the growing volume of research done by other people and companies. In 2016, I corralled a lot of these findings into a [book for O’Reilly](http://shop.oreilly.com/product/0636920041450.do). I also help curate WPOstats.com, which is a nifty [repository of performance research and case studies](https://wpostats.com/).

I work with Steve Souders and Mark Zeman at [SpeedCurve](https://speedcurve.com/), where we provide synthetic and real user performance monitoring to a huge spectrum of companies – from start-ups to household-name sites like Expedia and BBC. I’m also a chair of [O’Reilly Fluent](https://conferences.oreilly.com/fluent/fl-ca), which has a major focus on web performance.

> **One of the things that developers are often told they should worry about is page bloat. I know this is an issue that you've focused on a lot over the years, but recently you argued that it may not be as important a metric as we're led to believe. Can you briefly summarize why?**

I’ve been writing about page bloat for the past six years, ever since the average web page hit 1 Mb in size. At the time, that seemed incredible, though by today’s standards 1 MB would be considered pretty lean.

Last summer, when the average web page hit 3 MB, I [wrote a post](https://speedcurve.com/blog/web-performance-page-bloat/) that talked about why, if you care about user experience, page size isn't the right metric to track, because metrics like page size and load time aren't reliable indicators of user-perceived performance.

Take Amazon, for example. It's widely considered to be a performance leader, yet it has relatively heavy pages (defining "heavy" as 3MB or more) and slow load times (defining "slow" as 5 seconds or more). But for Amazon, page size and load time are the wrong metrics to look at. Looking at this performance test for the Amazon home page (which weighs in at just over 5MB), you can see a start render time of 1.4 seconds and a well-populated viewport at 2.5 seconds – despite the fact that the page doesn't fully load till 18.8 seconds.

![Amazon Page Weight](/images/posts/performance.png)

Now, having said all that, I should add that while page size may not be a relevant UX metric, it still matters a lot to users from a bandwidth perspective. You should also care about page bloat in terms of how it affects mobile users, especially mobile-only users who are dealing with bandwidth constraints or data limits. You should care even more if you have users who live in areas with significant connectivity issues. It’s so easy to forget just how poor networks can be in other parts of the world.

> **One of the things that I know I've often struggled with, and I think many other developers do as well, is missing the forest for the trees when it comes to web performance. I wonder if that's partly why page bloat became so important - because it distilled a bunch of issues (JS bloat, CSS bloat, image bloat) into an easy to understand number. I think developers have a tendency to focus on things like the performance of a specific JavaScript function or minor differences in the performance of various libraries and frameworks and overlook much more impactful fixes that may even take less time and effort. This is a long way of asking, do you believe that's true and, if so, what are some of the areas that you'd focus on first and foremost as a developer that can have the most direct impact on their site's performance?**

I think you’ve really hit the crux of it with this question. I talk with developers every day and I feel their pain. I completely see how with today’s massive, complex pages, it’s really hard to know what to focus on. You can’t optimize all the things, so how do you know where to optimize for maximum impact from your users' perspective?

Most performance issues can be lumped under three categories: images, blocking JS and CSS, and third parties.

Images make up the bulk of the average page, and you should definitely make sure you're not serving huge unoptimized images to your users. But this is one of those low-hanging fruit that's relatively easily addressable.

You should worry more about CSS and JavaScript. If you're serving asynchronous versions of your stylesheets and scripts, these have the potential to block your pages altogether, because they're major CPU hogs. Asynchronous scripts are better than synchronous, but there's an argument for deferring scripts (if you can wrangle it). And if you're not already measuring CPU usage, you should consider starting now.

Third parties are tricky because you don’t have complete control over them. But you do have more control than you might think. For example, you can monitor how they affect your pages over time and use that data to negotiate SLAs with your third-party providers. You don’t need to passively accept poor third-party behavior. That leads me to a really important point…

You can’t fix what you don’t measure. That saying has become an industry aphorism, because it’s true. You can obsess over libraries and frameworks all day long, but if at the end of the day you don’t know the impact that changes will have on how users perceive your site, you’re just obsessing in the dark. You need to focus on tracking the rendering metrics that matter most for your pages. Then you'll be able to see what UX impact, if any, your optimizations are having. 

If you're doing synthetic testing, then the best metrics to focus on are hero rendering times and Speed Index. If you're doing real user monitoring, then focus on custom metrics that measure the most important visual elements on your pages, such as product images or third-party ads. ([This post](https://speedcurve.com/blog/rendering-metrics/) does a good job of explaining and comparing the different rendering metrics.) 

> **You have often discussed how poor website  performance can have a negative impact on a business. The obvious impact would be things like abandoning a purchase, but what are some of the broader ways it can impact a company - even one that doesn't sell direct to consumers online?**

There are so many ways that performance has been proven to affect businesses: from brand perception and user retention to internal productivity and cost savings. 

In one study I worked on, we had all our participants engage with the same site. Half the participants had a relatively speedy experience, while we artificially throttled the site for the other half. The people who had the slower experience didn't just perceive the site as being slower: they also reported that they considered the content, design, and navigation to be poor. In other words, the site's slowness gave them an overall negative perception of the entire site. 

From a cost savings perspective, a couple of years ago Wikipedia reported that they deployed new technology that sped up their underlying PHP-based code and ultimately improved load times by about 66%. It also allowed them to radically cut back on new server costs. Netflix saw a 43% decrease in its monthly bandwidth bill after it enabled gzip and reduced payload by more than half. 

I could go on and on. One thing I've learned over the years: if you can name a business metric, then you can probably map it to performance in some quantifiable way. I have yet to find a metric that defies mapping.

> **I am excited to see Tammy speak this Wednesday and hopefully you are too. Join us at [Improving Your Apps - Performance and Debugging](https://certifiedfreshevents.com/events/improving-your-apps/)!**