---
layout: post
title: "On The Mobile Web in Mobile Web Weekly"
date: "2016-08-25"
categories: 
    - web development
    - mobile
description: Addressing the controversy over the links in Mobile Web Weekly.
comments: true
---

There has been quite a bit of debate stirred lately about the content in the [Mobile Web Weekly newsletter](http://mobilewebweekly.co/) (which I co-edit with Holly Schinsky and is run by Cooper Press). In part, the debate was stirred by a fair question from Paul Irish:

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr"><a href="https://twitter.com/remotesynth">@remotesynth</a> i noticed a distinct lack of &quot;mobile web&quot; in this week&#39;s &quot;mobile web weekly&quot;. what&#39;s goin on?</p>&mdash; Paul Irish (@paul_irish) <a href="https://twitter.com/paul_irish/status/768538722220376064">August 24, 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

You can see some of my responses to his tweet, but I wanted to discuss it more here as there's more to say than can fit into a tweet or two.

First, some background on Mobile Web Weekly.<!--more-->

## How Mobile Web Weekly Began

I start here because it ultimately helps to understand where the initial vision for the newsletter came to be. I initially proposed the idea to Peter Cooper over 4 years or so ago, when I worked for Adobe.

At the time, I was publishing a lot of content around responsive web design and PhoneGap/Cordova. However, unlike when I published JavaScript content (which had JavaScript Weekly) or CSS content (which had CSS Weekly), there was no obvious place for this content to go. HTML5 Weekly (now Front End Focus) did exist, but was firmly focused on the actual features in the HTML5+ specs, not mobile web or hybrid development.

The initial plan was that this would even be sponsored by PhoneGap/Adobe. In the end, I was unable to secure the funding, but the idea never died. Eventually, Peter and I decided to move forward with it, and we invited Holly due in part to her expertise in hybrid mobile development.

The point of this background is that the newsletter always had a focus on _web technologies for mobile development_ and not just mobile web browser development. Peter, Holly and I even debated this when trying to name it, but Mobile Web Tech Weekly sounded awkward and confusing. Mobile Development Weekly sounded like it would cover native development, which felt like too broad a topic to be useful for a newsletter.

## How Things Have Changed

3 years ago when the newsletter started, things were a little different. There was mobile web development (namely RWD) and hybrid development (i.e. Cordova). No one seemed to care that the newsletter often would have a heavy amount of hybrid.

Since then, tools like React Native, NativeScript and others have come about that also use web technologies to build for mobile, but in a decidedly different manner than even hybrid. The result is a native app (a native UI) with web technology hidden from view, underneath the covers.

But that's not the only change that has happened. The other is that the "mobile web" has somewhat disappeared as a thing. Web design is responsive web design nowadays. Many authors don't even make a distinction about whether their topic covers mobile - it's assumed that the web _is_ the mobile web. It's a distinction without a difference in many cases.

Except, when it isn't. Things like progressive web apps and AMP, both initiatives from Google, are decidedly geared towards the mobile web. We've covered these topics extensively - so much so, that I worried we were over-covering them. For all the debate about [this week's issue](http://mobilewebweekly.co/issues/122), check [last week's](http://mobilewebweekly.co/issues/121), which had a lot of PWA and web-browser focus. In fact, I'd argue that if you [go through the archive](http://mobilewebweekly.co/issues), you'll find that this week's very heavy focus on things like React Native, NativeScript and Cordova is more an aberration than a trend.

But something else has changed along with the technologies, and that is the audience.

## Technology has Become Much More Partisan

Paul Irish alluded to this somewhat in one of his responses, though he is more focused on the semantics of the newsletter's name and what it implied in terms of content:

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr"><a href="https://twitter.com/peterc">@peterc</a> <a href="https://twitter.com/remotesynth">@remotesynth</a> it the same way: the &quot;app or web&quot; choice. To me, Hybrid/ReactNative feel like a great _alternative_ to the &quot;mobile web&quot;</p>&mdash; Paul Irish (@paul_irish) <a href="https://twitter.com/paul_irish/status/768584905924018176">August 24, 2016</a></blockquote>

Matthewcp laid it out much more straightforwardly.

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr"><a href="https://twitter.com/peterc">@peterc</a> <a href="https://twitter.com/remotesynth">@remotesynth</a> <a href="https://twitter.com/paul_irish">@paul_irish</a> the community has fractured between JS devs and Web devs. JS side more open to the native stuff. Not I.</p>&mdash; matthewcp (@matthewcp) <a href="https://twitter.com/matthewcp/status/768635809570385925">August 25, 2016</a></blockquote>

Back when the newsletter started, no one seemed bothered by its occasionally heavy focus on hybrid. This was probably because hybrid was considered a stopgap - a way to build for mobile and compete with mobile app ecosystems until the web finally caught up.

Nowadays, with HTML5 being so ubiquitous it isn't really even a "thing" and with efforts like PWAs and AMP, many people feel that the web has nearly caught up and we don't need things like Cordova/React Native/NativeScript to compete. They would argue that we just need to go all in on mobile web to get us across that finish line.

Others seem to believe that it has been years, and the web, while fractured, is still trying to catch up - and will continue to do so. They would argue something along the lines that we were promised parity with HTML5 but the web seems as fractured or more today - even PWAs, for instance, only target recent Android.

## Can We Serve Multiple "Communities"?

The bigger question I think both Paul and Matthew are getting at is (beyond the specifics of the naming of the newsletter) _can we have a newsletter that serves both audiences?_ Can the two sides coexist? Or, much like TV and news today, do we need to target some micro-community, making a newsletter for mobile web, one for hybrid and one for React Native/NativeScript/Tabris.js/etc?

Personally, I would love to keep things as is. I think retreating further into a specific technology corner only makes the issues worse. We probably can and should do a better job of balancing the content, making the purpose clear and maybe sectioning the content so that it is more apparent what topic areas are covered. Perhaps we even should rename the newsletter. But I still think that a single newsletter can serve this whole audience and that by doing so we keep developers better aware of the larger ecosystem of tools and issues for using web technologies to target mobile.

Obviously, I am not the only voice here. Peter and Holly have been and will continue to be part of this discussion as it pertains to the newsletter. As the audience, I'd also love to hear your opinions.