---
layout: post
title: "A License to Confuse"
date: "2018-01-29"
categories:
    - general
description: More evidence that developers aren't noticing the licenses in the software they use.
comments: true
---

A while back I wrote a post suggesting that [developers need to start paying attention to licenses](https://www.remotesynthesis.com/blog/developers-and-licenses). It was inspired, in part, by the whole [React licensing brouhaha](https://heathermeeker.com/2017/08/19/open-source-community-over-reacts-to-x-rated-code/).

What inspired me about that controversy was not the specifics of the React license itself (which was a version of a [BSD + patents](BSD+Patent) license) but the fact that this license had been in use by the React library since October, 2014 - nearly 3 years before the controversy came to light when the library moved from an Apache v2 license. There were stories of large enterprises looking to rip React out of complex applications because of this controversy, which could be a massive and expensive endeavor, for a problem that was readily avoidable.

Now, you can argue that this was seriously overblown (what else is new?) and that Facebook has since rectified this anyway by moving to the very liberal MIT license. However, my curiosity was more "How did it take 3 years for anyone to notice?"

## So Why Bring This Up Again?

I recently got accepted to present on this very topic to [Fluent Conference in San Jose](https://conferences.oreilly.com/fluent/fl-ca) this June. I was doing a little preliminary research for my talk and became aware that React Native is still on the same controversial BSD + patents license.

In fact, I ran a diff on the [React license and patents pre-sept 25](https://raw.githubusercontent.com/facebook/react/bef45b0b1a98ea9b472ba664d955a039cf2f8068/LICENSE) and [current React Native license](https://raw.githubusercontent.com/facebook/react-native/master/LICENSE) as well as the patents grant and they are identical. The only difference is the name of the software and the year of the copyright.

Yet, there doesn't seem to be any outrage over the license. In fact, according to the [State of JavaScript](https://stateofjs.com/2017/mobile/results) survey results, more than 4.8k developers have used React Native and plan to use it again and another 14k respondents would like to learn and use it.

![JavaScript mobile library stats](/images/posts/mobile-library-use.jpg)

It's not that _nobody_ has noticed. Paul Chong brought it up on a [post on Medium](https://medium.com/@paulhyunchong/react-native-is-not-under-the-mit-license-54308f8b26ed), for example. And some people brought it up on a [GitHub issue has since been closed](https://github.com/facebook/react-native/issues/16079) with [no indication of a pending change](https://github.com/facebook/react-native/issues/16079#issuecomment-335855158). But if the controversy was warranted with regard to React, why not React Native?

> Full disclosure: I work for Progress Software, who create the NativeScript project that competes with React Native. However, I want to state that I am not here to discuss either the merits of the license or the project itself, just how the inconsistencies in the reaction of the community illustrate a potential lack of awareness around licenses in general.

## My Theories

I have a few potential theories.

1. **Most developers realized that the initial controversy was seriously overblown and have adjusted their expectations.** This seems unlikely. The initial controversy didn't subside until React changed its license. The explanations pushed at the time for the use of BSD + patents did little to quell the outrage, even if it was arguably overblown or even undeserved.
2. **Most developers or enterprises have differing expectations of a mobile framework than a web framework.** Honestly, this would make no sense whatsoever. Whether justified or not, the arguments made about its broad patent revocation clause (the reason React landed on Apache's [category x](https://www.apache.org/legal/resolved.html#category-x)) would apply equally to a mobile app as to a web app.
3. **Most developers are unaware that the license differs from React and simply assume that it is the same.** Yep, my money is on this one.

I've seen this occur both in my own work experience and throughout the industry as it relates to dual-licensed software. Very often, developers (and many companies) remain unaware of the various stipulations related to the open source version's usage and simply assume open-source===free. In this case, the software is not dual-licensed, but it is not illogical for a developer to assume that since React is MIT licensed (assuming the developer is even aware of the React license), then React Native would be too...so why even look at the license?

I'm not arguing that in this specific case, it could get your company into potential trouble - again, I'm not here to debate the merits of this specific license. However, it is exactly this very _type_ of case - one where we, as developers, adopt tools that we are not aware of the licenses of - that could cause problems.

I hope to look into this whole process more as I continue to prepare for the talk in June. I'd love to hear your thoughts and feedback to guide me as I prepare.