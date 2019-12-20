---
layout: post
title: Thoughts on the State of JS Survey
date: '2019-12-20'
description: A look at the latest edition of the largest JavaScript developer survey.
categories:
  - javascript
comments: true
---

The [latest State of JS survey results](https://2019.stateofjs.com/) are out. As always, survey results need to be taken with a grain of salt. There is always a bit of [selection bias](https://en.wikipedia.org/wiki/Selection_bias) involved in these sorts of surveys whereby certain groups tend to be far more likely to respond. These concerns are somewhat reinforced by the survey's own reporting wherein almost 70% of respondents came from 3 sources.

[![State of JavaScript response source](/images/posts/state-of-js-2019/source_sm.png)](https://2019.stateofjs.com/demographics/#source)

As another example of this, the survey was [91.3% male](https://2019.stateofjs.com/demographics/gender). While people who identify as women or non-binary are severely underrepresented in our industry, the [latest information](https://www.inc.com/laura-garnett/women-in-tech-what-s-the-status.html) would put the percentage more likely in the 15-17% range.

All those caveats aside, this is the largest survey focused exclusively on JavaScript, with 21,717 responses, so it can be interesting to parse the results and see how they align with your own opinions and perceptions of the community. Not a ton surprised me this year, but here are some somewhat random things that stood out to me when reading it.

> For a very different take, check out [this post by Jerod Santo](https://changelog.com/posts/7-insights-from-the-state-of-js-2019).

## We Overstate Our Expertise

The survey does not seem to have asked people to state their JavaScript proficiency, but, considering the target audience, it's probably safe to assume they lean advanced or expert with JavaScript. So it is a bit surprising that 56.4% of respondents consider themselves to be either advanced or expert in CSS, including about 40% saying they are a CSS expert.

[![CSS Proficiency](/images/posts/state-of-js-2019/cssProficiency_sm.png)](https://2019.stateofjs.com/demographics/cssProficiency)

In addition, 64.9% say they are advanced or expert in back-end, though trending slightly towards advanced over expert.

[![Backend Proficiency](/images/posts/state-of-js-2019/backendProficiency_sm.png)](https://2019.stateofjs.com/demographics/backendProficiency)

These results would indicate that a majority of respondents likely see themselves as advanced or expert in JavaScript, CSS and backend development. The survey laid out pretty high standards for these definitions (as seen in the images above). Even accounting for just over 50% of respondents having over 5 [years of experience with JavaScript](https://2019.stateofjs.com/demographics/workExperience) (which, for the record also seems unusually high), color me extremely dubious.

## Rankings? 🤔

The survey displays a section it calls "rankings" for frameworks. The way this is displayed shows Vue (87%), Svelte (88%) and React (89%) sitting almost even for frontend frameworks.

[![front end framework rankings](/images/posts/state-of-js-2019/front_end_frameworks_experience_ranking_sm.png)](https://2019.stateofjs.com/front-end-frameworks/front_end_frameworks_experience_ranking)

This struck me as odd. Sure, Svelte has had a lot of momentum lately, but having it ranked almost tied with React, above Vue and well above Angular seemed off. However, the problem wasn't the data here so much as the terminology and the choice of how to display it. I think it can lead to misunderstandings, as it did initially with me.

The results above are only for a "satisfaction" ratio. There is a menu of options that, at least to me, wasn't initially obvious that allows you to switch to interest and awareness ratios. I believe the choice of "rankings" for the heading was chosen because these stats were grouped together, but I think it only compounds the initial confusion and potential misinterpretation.

Once I understood the way this was displayed, there were few surprises in the results. Same for back end frameworks.

[![backend framework rankings](/images/posts/state-of-js-2019/back_end_frameworks_section_overview_sm.png)](https://2019.stateofjs.com/back-end/back_end_frameworks_section_overview)

Perhaps the only surprise was the popularity of Next.js and how quickly Meteor has fallen out of favor. In fact, my biggest surprise was in the [mobile and desktop](https://2019.stateofjs.com/mobile-desktop/) rankings.

[![Mobile and desktop](/images/posts/state-of-js-2019/mobile_desktop_experience_ranking_sm.png)](https://2019.stateofjs.com/mobile-desktop/)

NativeScript isn't even on the list. Perhaps I have a bias there myself since I worked at the company that makes it, but the [other tools](https://2019.stateofjs.com/mobile-desktop/other-tools/) results seem to show it was a major missed inclusion as were others including, arguably, PWA even if it encompasses a range of tool solutions. Flutter may have been a big miss as well since the target audience seems to be partly JavaScript developers as it's not like there's a State of Dart survey.

## Where Do We Go to Learn?

As someone who focuses on creating developer content, it's always interesting to me to see where developers are going to learn and keep up with their field. CSS Tricks has a substantial lead over everyone else with Dev.to coming in second. I was a bit surprised to see both beating out JavaScript Weekly as getting a top link in that newsletter seems to bring in large amounts of traffic, but maybe folks think of it as more of a secondary source since the content resides elsewhere.

[![blogs and magazines](/images/posts/state-of-js-2019/blogs_news_magazines_sm.png)](https://2019.stateofjs.com/resources/blogs_news_magazines)

Medium received a lot of votes in the freeform answers, even despite the dreaded paywall. I was also still surprised that almost 20% still consult W3Schools, barely trailing MDN which is a far better resource. There are lots of folks that seem to be using Udemy, Egghead.io and FrontEndMasters. That doesn't surprise me, but no mention of Pluralsight at all? That does.

## Opinions on JavaScript

Most of the data in the [opinions](https://2019.stateofjs.com/opinions/) section didn't surprise me. Folks seem to think things are headed in the right direction, though they feel less strongly about it than in years prior. I was a little surprised that most respondents do not agree that building JavaScript apps has gotten too complex now - only 40.3% either agree or strongly agree.

[![JavaScript too complex](/images/posts/state-of-js-2019/building_js_apps_overly_complex_sm.png)](https://2019.stateofjs.com/opinions/building_js_apps_overly_complex)

I thought the percentage would be higher. But I suppose we've already learned that a big chunk of respondents area apparently experts in everything related to the web, so maybe I shouldn't have been surprised.

Notably, the percentage of folks who think JavaScript is changing too fast has dropped, even though technically the language changes every year now. This doesn't terribly surprise me. ES6 was a major shift that took folks time to adjust to. However, recent changes are much less dramatic. I also feel as though the sense that there is a new framework every week has cooled.

[![Ecosystem rate of change](/images/posts/state-of-js-2019/js_ecosystem_changing_to_fast_sm.png)](https://2019.stateofjs.com/opinions/#js_ecosystem_changing_to_fast)

## What to Make of It?

It is fun to delve into these and, despite any complaints, am grateful for the folks who put this together. It is a lot of work. It can be useful to challenge some assumptions you may have, learn about new technologies you perhaps hadn't heard of and try to pick up on trends. However, I don't think there is anything in here that should cause anyone to make major changes to the way they do things or the tools that they use.