---
layout: post
title: Technical Debt is Not Just Technical
date: '2019-07-19'
description: Many factors can influence technical debt and many of them have nothing to do with code.
categories:
  - general
comments: true
---

I'm going to admit something kind of embarrassing here. Looking back on my career, I believe that there were times relatively early in my career when I was probably difficult to work with. I believe I've learned from those mistakes. Let me explain.

## Technical Debt

Developers often refer to the concept of [technical debt](https://martinfowler.com/bliki/TechnicalDebt.html). Essentially technical debt is the "cruft" that gets leftover in an application due to some poor initial decisions about how it was built. These choices are sometimes made deliberately and sometimes unintentional. The thing about technical debt is that it often builds upon itself - poor choices initially limit the choices down the line so that it can ultimately become extremely painful, difficult and, yes, costly to correct.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">“This technical debt can wait. I have a feature to deliver!” <a href="https://t.co/OrUZgGUbwV">pic.twitter.com/OrUZgGUbwV</a></p>&mdash; Changelog (@changelog) <a href="https://twitter.com/changelog/status/1103511794855936000?ref_src=twsrc%5Etfw">March 7, 2019</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

The other thing about technical debt, it is often much easier to see when you are new to a company or project - especially the unintentional kind.

## Misdiagnosis

So, here's me, circa 2005 or so, armed with the confidence of some years as a developer under my belt. My newness to the companies (yeah, I bounced around a bit at this time in my career) made it relatively easy to recognize technical debt. From a technical standpoint, I had enough knowledge to diagnose the issues.

But here's the thing about technical debt which I only learned through years of painful experience - despite its name, technical debt is not just technical. It is organizational, institutional, political and, yes, often personal.

Behind every bit of technical debt, there is a story. Sometimes the story can be simple like, "Oh crap! I didn't realize it should be done this way." More often though, there is a much more complex story that involves people whose egos may be on the line, organizations who pushed for solutions for reasons that aren't technical (an example would be "[dogfooding](https://en.wikipedia.org/wiki/Eating_your_own_dog_food)" or software choices mandated by a purchase a senior manager made from a buddy). Sometimes technical choices can be wrapped up in such a complex history that it can become difficult to unravel exactly how the choice was made.

[![The other infinite loop that all coders fear](/images/posts/infinite-loop.jpg)](http://www.commitstrip.com/en/2014/09/08/the-other-infinite-loop-that-all-coders-fear/)

The point here is, 2005 me had learned enough to diagnose and, perhaps, even fix these issues at the companies I was joining from a technical standpoint. Armed with technical knowledge I jumped in head-first only to land on powerful blockers that were not technical in nature. My failure was in not being able to see and diagnose the non-technical aspects of the technical debt and this failure left me often frustrated.

## Learning to Listen

Basically, I had a "code first ask questions later mentality" when the answer was simple - take the time to ask questions and listen. Find out why certain choices were made. Doing so gives me the knowledge I need to diagnose the technical problem (and to my surprise, sometimes better understanding the non-technical reasons made me realize I was actually misdiagnosing something as technical debt). But, more importantly, it enabled me to offer solutions that work not just from a code standpoint, but work for the people I have to work with and the company I am working for.

Remember that asking questions and listening takes time and patience. You cannot come in thinking you have all the answers, as I did. The best analogy I can think of is going to a doctor to treat pain. The doctor can quickly treat the symptom and the pain will subside, but can leave the problem to fester undetected. However, a good doctor will take the time to understand you, your issues and investigate the underlying causes of the pain and treat it holistically. Be the good doctor that circa 2005 me was not.