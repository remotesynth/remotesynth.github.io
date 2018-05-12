---
layout: post
title: "What Developers Should Know from Microsoft Build"
date: "2018-05-12"
categories:
    - general
description: We're clearly entering a new era for Microsoft and for developers
comments: true
---

It used to be that I could easily ignore the news coming from Redmond. Sure, Microsoft was always important, but I was never a .NET or Windows developer, so what they were saying rarely applied to me. I might be impressed by the quality of their tooling, like Visual Studio, but I didn't write C#, so it didn't really matter.

That's not the case nowadays. Microsoft has an outsize role in most every developer's career. Even if you don't directly use their products or services, the direction they take has an enormous impact on us. For example, as they recently touted, they are the largest corporate contributor to open source on GitHub.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Microsoft is the largest single corporate contributor to open source on Github. <a href="https://twitter.com/hashtag/MSBuild?src=hash&amp;ref_src=twsrc%5Etfw">#MSBuild</a> <a href="https://t.co/Z3ugzLSRul">https://t.co/Z3ugzLSRul</a> <a href="https://t.co/WXSuF7NQhg">pic.twitter.com/WXSuF7NQhg</a></p>&mdash; Microsoft Developer (@msdev) <a href="https://twitter.com/msdev/status/993546257988833280?ref_src=twsrc%5Etfw">May 7, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

That's just one of the signs of a different Microsoft. In this post, I will share some of my own observations and thoughts after attending this week's Microsoft Build conference in Seattle. I won't spend a lot of time diving into the big announcements, but more on a general view of where I see Microsoft heading and how that impacts us as developers.

## How Times Have Changed!

I know everyone talks about the "new Microsoft" but it was truly evident at this event in so many ways. Let me illustrate a few:

* Microsoft frequently touted its Linux support within various products and services (including the support for Linux line endings in Notepad that was, somewhat improbably, the biggest applause line of the keynotes).

* Microsoft brought Amazon on stage to demonstrate their Cortana/Alexa integration (which was somewhat underwhelming, but you need to start somewhere I suppose). Yes, the same Amazon who is their biggest competitor in cloud services.

	<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Alexa and Cortana working together? Amazon and Microsoft up on stage together at <a href="https://twitter.com/hashtag/MSBuild?src=hash&amp;ref_src=twsrc%5Etfw">#MSBuild</a> showing Cortana running on an Echo and Alexa on Windows. <a href="https://t.co/C3kmHCWgMr">pic.twitter.com/C3kmHCWgMr</a></p>&mdash; Brian Rinaldi (@remotesynth) <a href="https://twitter.com/remotesynth/status/993530284304879618?ref_src=twsrc%5Etfw">May 7, 2018</a></blockquote>

* The second day keynote began with a mention that they would work to be done in time for the Google I/O keynote to begin so that viewers could switch over.

In my view, Windows and .NET played a very small role in either the day one or day two keynotes. In most cases, they played a supporting role for other announcements - in some cases a very important supporting role, but not the focus.

In fact, Microsoft seems to have accepted the reality that many/most (not sure which) developers choose to develop on a Mac. For instance, one of my personal favorite demos of the keynotes was something called [Visual Studio Live Share](https://www.visualstudio.com/services/live-share/), which enables incredible, real-time collaboration between developers (something that could be a game changer for distributed teams). The key thing about the tool though is that it doesn't care if you are working on a Mac or a PC (using either Visual Studio or Visual Studio Code).

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Visual Studio Liveshare sharing code, editing and interaction between Visual Studio Code on a Mac with Visual Studio on Windows. <a href="https://twitter.com/hashtag/MSBuild?src=hash&amp;ref_src=twsrc%5Etfw">#MSBuild</a> <a href="https://t.co/hWc8UyvlbZ">pic.twitter.com/hWc8UyvlbZ</a></p>&mdash; Brian Rinaldi (@remotesynth) <a href="https://twitter.com/remotesynth/status/993543376971616256?ref_src=twsrc%5Etfw">May 7, 2018</a></blockquote>

As with most of the things Microsoft showed related to tooling, this was free, which may lead you to ask how and why they do that.

## The Changing Landscape of Developer Tooling and Services

While I had this sense already, it became much clearer to me throughout Build that Microsoft is what you might call a "cloud first" company. By this I mean that everything, including things like Windows and Office, are moving towards a future whereby they support the core business of Azure.

I don't know enough about Microsoft's financials to know how big a role Azure services play in their current financials, but it is clear that this is where they see the growth and their future. This means that software, hardware and tooling are the three legs of the stool holding up their ever expanding cloud offerings by serving as the hooks that bring you into the ecosystem.

In my view, even their announcements that didn't even seem to be directly about Azure, were about Azure. Let me show a couple examples.

* There was a lot of talk about AR, VR and drones. In some cases, this seemed to focus on Microsoft's hardware, in particular the HoloLens.

	<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Microsoft Remote Assist is a really clever and, more importantly, useful looking use of AR using HoloLens. I could see this having broad appeal. <a href="https://twitter.com/hashtag/MSBuild?src=hash&amp;ref_src=twsrc%5Etfw">#MSBuild</a></p>&mdash; Brian Rinaldi (@remotesynth) <a href="https://twitter.com/remotesynth/status/993533735252312064?ref_src=twsrc%5Etfw">May 7, 2018</a></blockquote>

	However, it seems clear that Microsoft does not see the HoloLens hardware as the key here. The HoloLens is just a tool that ties into an array of services (machine learning and artificial intelligence) that are the engine allowing the hardware to do anything useful. Today the hardware is from Microsoft - probably to prove the concept - but tomorrow it could be anyone's hardware so long as Azure is the engine that makes it run.
* There was quite a bit of talk (especially on the day 2 keynote) about Office, however it was all centered around this concept of the "office of the future." This was an office where every meeting and every conversation relied upon machine learning and AI services from Azure. Even seemingly unrelated Office announcements seemed to actually be about Azure.

	<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Micosoft announcing custom functions for Excel that live in the cloud and written in JavaScript. <a href="https://twitter.com/hashtag/MSBuild?src=hash&amp;ref_src=twsrc%5Etfw">#MSBuild</a></p>&mdash; Brian Rinaldi (@remotesynth) <a href="https://twitter.com/remotesynth/status/993891768432082945?ref_src=twsrc%5Etfw">May 8, 2018</a></blockquote>

	Why would Microsoft allow you to write Excel functions in JavaScript? Not because they love JavaScript, but because a) they live in the cloud and b) they then connect to other Azure services. Little by little, things like Excel just become containers for building complex, task-based business services that rely on the Azure cloud.

## The Takeaway for Developers

In my opinion, the important thing for developers to understand here is that Microsoft is headed in directions that may fundamentally change our roles (and where they are going, others are going too). They are no longer purely interested in us building applications on their platforms using their tools. In the old scenario, of tools and platforms, we developers would essentially drive the car off the lot and only come back for the occasional service appointment (via a support subscription or software upgrade).

They want us building applications that rely on their services, whether we use their tools or not. In this analogy, our car might be off the Microsoft lot or off a different lot altogether, but every time we turn the ignition or turn on the radio or hit the brakes, we depend on Microsoft.

I'm not saying that this is a bad change - not having to build out server infrastructure or reinvent the wheel for many complex code tasks means that we can accomplish things that in the past may have been out of reach. But we should be aware of how these changes in the industry are going to dramatically change what is expected of developers.
