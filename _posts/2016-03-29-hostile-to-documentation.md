---
layout: post
title: "Hostile to Documentation?"
date: "2016-03-29"
categories: general
description: Developers don't like writing documentation.
comments: true
---

I think every developer has had that feeling when they discover a project on GitHub that seems like the answer to the problem they are trying to solve. Unfortunately, many times this project turns out to be either undocumented or minimally documented and the experience ends in frustration.

Yesterday I released an article titled "[Your Open Source Project is Considered Harmful](http://developer.telerik.com/featured/open-source-project-considered-harmful/)" (fwiw, the title is meant to be cheeky though not everyone took it that way) that discusses the huge abundance of undocumented and poorly documented code on GitHub. The goal of the article is to ask developers to think before they make their code public - and if you are just posting a project that you don't intend to maintain, support or document, make that clear to the end user.

I knew that the topic would be somewhat controversial but I didn't realize the level of hostility and sometimes anger (towards me specifically) it would engender. I want to take a moment to discuss some of the responses.<!--more-->

## It's the User's Problem

Many responses seemed to think that it is the user's responsibility to write documentation if they feel it is needed.

> "The problem is people using a project, but not contributing to documentation."
>
> \- [Comment from The Engineer](http://developer.telerik.com/featured/open-source-project-considered-harmful/#comment-2593324936)

This seems to relate to a sense of altruism - I created this code for the benefit of you (i.e. the developer community). By asking more of me, you are being ungrateful.


> It’s helping people willing to do the work to figure out if the project is useful to them. Sorry if that isn’t you, but the author is under no obligation to appease anyone.
> 
> \- [Comment from zeebo](https://lobste.rs/c/oxnhwy)

A similar sentiment was occassionally expressed in a more hostile manner.

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr">Actually <a href="https://twitter.com/Telerik">@telerik</a>, maybe your attitude and sense of entitlement is harmful <a href="https://t.co/B2XhmIwO1C">https://t.co/B2XhmIwO1C</a></p>&mdash; Imperator Pathogen (@sandfoxthat) <a href="https://twitter.com/sandfoxthat/status/714746046346342400">March 29, 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

I do believe that most developers share their code in large part out of a sense of altruism. Sure, in many cases, we wouldn't mind the attention of our peers, but I think the overriding sense is that it is good for the community to share our code. I understand that no one likes to be told that their "gift" is unwanted - and, in some respects, that is what I am being perceived to be doing.

What I am unclear on here is why a developer with such good intentions wouldn't want to make even a minimal effort to ensure their "gift" is well received. I wouldn't give someone a gift and hand them half the bill - but by only writing the code but not the documentation, you've left half the bill unpaid. As I said in the article, this will also help you determine "why anyone outside of yourself would need it. What problem does it solve? Who is the target audience (ex. what skills are needed to use it)? And even, what do I hope to gain by sharing this and how committed am I to maintaining it for the community?"

If the project is a personal project and you don't really intend to maintain it, document it or support it - it seems pretty easy to make that clear in the readme. If the project is purely experimental and not intended for production use, make that clear - even if your plans may change. If a user still decides to use it, they do so well aware of the risks.

## The Risks Are Obvious

Many other commenters seem to believe that the risks of using undocumented code are obvious and, in effect, the user is already well aware of the developer's intention.

> Disagree with the conclusion, the answer is much simpler. As a rule, if the project isn’t documented just assume it probably isn’t suitable for public use and certainly isn’t suitable for production use.
>
> \- [Comment from sdiehl](https://lobste.rs/c/q58sv7)

Others also make it clear that the onus is on the user - and that since the developer can't know how the user intends to use the code, it's up to the user to document it if they wish, should they choose to use it.

> Many users shared your frustrations, but they’re still users. Their frustrations with the project must be less than whatever frustrations drove them to use someone’s undocumented code. If enough people find this code useful, maybe they’ll consider contributing documentation back to the code base as they figure it out. If the author sees this, they may realize that if people find the undocumented draft project useful, that maybe it’s worth some effort to improve it. Or the author doesn’t care, someone forks the project, and it takes off.
> 
> There are many paths to useful open-source projects, and they don’t all require the author to spend an inordinate amount of time documenting every feature for a project nobody may ever see. The onus on deciding how to put together your project is still on you, not the authors of every piece of open-source code that might be relevant to your project.
> 
> \- [Comment from ericdykstra](https://lobste.rs/c/kfaq2a)

Other say that if you ue a project with little or poor documentation, it's due to a lack of due diligence (and, again, if you want documentation, write it yourself).

> It really is not that hard to instead of just searching for all available projects, talk to some peers and see what mature options are out there, or do the ‘research" yourself. If it is a good product and there is no documentation, and that’s a problem for you, write some.
> 
> \- [Comment from voronoipotato](https://lobste.rs/c/wltdis)

The issue I have here is that it is not always so cut and dry. I'm going to use two examples from the world of static site generators (because I spend a lot of time with them). Please note, I am not meaning to pick on the authors who dedicated time to these projects - just to give an example of where, I believe, the lack of documentation is not so obvious and, in my opinion, hurts potentially strong projects.

If you look at [Wintersmith](http://wintersmith.io/) you'll see that there is a good overview and even a getting started guide. However, once you get past the getting started guide, unfortunately, there is little else. I have built projects using Wintersmith and spent a lot of time digging through the code to figure things out. In many cases, I spent far more time than otherwise would have been necessary in order to figure out a simple feature due to the lack of documentation. The thing is, I actually generally like Wintersmith, but the lack of documentatin makes it harder to recommend it.

Another example is [Metalsmith](http://www.metalsmith.io/). It also has a nice home page. It includes basic installation and configuration documentation for the base project and for most of the plugins I researched. It does not have any form of usage documentation (yes, it has a few sample projects, but these are so incredibly simplistic that they are not very useful).

Both of these examples are of potentially strong projects that are a) not obviously undocumented and b) hurt by their lack of documentation. A quick perusal of the issues on projects like these show that misunderstandings are common due to a lack of documentation.

## Community Contribution

This doesn't mean that you, the project owner, need to document absolutely everything, even if you intend your project for public consumption. But I'd argue that you should have at least the basics of installation, configuration and usage that cover at least the primary use cases for your tool. It's ok to rely on the community to expand the docs to meet more use cases or cover deeper topics, but without giving them at least the basics to start with, I can't actually forsee that happening.

Again, if this project is still in development, is intended primarily for personal use, or is purely experimental - just say so.

I do believe that users should contribute more to documentation. In fact, this is something I have [publicly discussed before](https://www.youtube.com/watch?v=VtFbMhm8z9A). But it starts with us as a community (including OSS developers) **valuing documentation**, and the "if you want documentation so bad, write it yourself" attitude that seems pervasive in the comments makes it clear that we don't value documentation. Instead, that potential documentation contributor to your project is off writing their own project and posting it to GitHub.

Offering contributon guidelines specifically for documentation (as [some](https://contribute.jquery.org/documentation/) [projects](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#-found-an-issue) [do](https://jekyllrb.com/docs/contributing/#ways-to-contribute)) can both encourage participation and show that you value documentation.

## Overall a Good Discussion

I should be clear, though, that most of the comments on the article were extremely thoughtful and constructive. In fact, I reworded some of my suggestions as they obviously came across more prescriptive and black-and-white than I'd intended. The goal of the post was simply to get people thinking of the importance of documentation and the potential cost to the very community that these projects aim to help simply by not including it. Despite some hurt feelings and angry reactions, hopefully I was able to at least start a conversation.



