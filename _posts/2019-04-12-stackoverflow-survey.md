---
layout: post
title: "Some Things You May Have Missed in the Stack Overflow Developer Survey (2019 Edition)"
date: "2019-04-09"
categories:
    - general
    - web development
description: A quick look at some highlights from the latest edition of StackOverflow's survey
comments: true
---

With over 90,000 responses, the Stack Overflow Developer Survey is the largest survey targeting the developer community. This doesn't mean the results are perfectly reflective of the developer community (something, StackOverflow themselves acknowledge), but they are a useful metric to gauge certain aspects of the community - from changes to the make up of the community itself to interests and job focus.

Last year, I took a look at some items that [stood out to me](https://dev.to/remotesynth/some-things-you-may-have-missed-in-the-stack-overflow-developer-survey-40lo), and following the recent release of [this year's results](https://insights.stackoverflow.com/survey/2019#developer-profile-_-social-media-use), I'd like to do the same.

Please note that these are only the items that struck me. I invite you to share your own insights in the comments or in a post of your own.

## Some Changes in Methodology This Year

StackOverflow has received its fair share of criticism over the years regarding its community. Last year they started to make a public effort to [respond to those criticisms](https://stackoverflow.blog/2018/04/26/stack-overflow-isnt-very-welcoming-its-time-for-that-to-change/). I'm not here to judge the success or failure of those efforts on a larger scale, but it did impact the way they handled the survey results.

Firstly, they acknowledge the issue up front:

> Despite our survey’s broad reach and capacity for informing valuable conclusions, we acknowledge that our results don’t represent everyone in the developer community evenly. We have further work to do to make Stack Overflow the welcoming, inclusive, and diverse platform we want it to be, and this is reflected in our survey sample.

Secondly, they decided to release weighted results that attempt to correct the demographic skew. Thus you get results like the unweighted [developer roles](https://insights.stackoverflow.com/survey/2019#developer-roles) in the United states...

![developer type unweighted](/images/posts/stackoverflow2019/developer-type-unweighted.png)

...and weighted:

![developer type weighted](/images/posts/stackoverflow2019/developer-type-weighted.png)

In some cases, the results don't change much but in others it can give interesting insights. For instance, above you'll see some slight changes in the overall percentages of the top 5 items. However, after that, the weighting actually changes the order, with designer moving above both database admin and DevOps, even if the overall percentage change is still relatively small.

A big part of the skew is [gender-related](https://insights.stackoverflow.com/survey/2019#developer-profile-_-gender). Yes, the industry-wide numbers are bad (with [some data](https://www.evia.events/info-women-in-technology) putting women at less than 20% of tech jobs overall and many reports showing those numbers declining) but StackOverflow's responses are over 91% men overall and just 11.7% women even in the US.

![gender makeup](/images/posts/stackoverflow2019/gender.png)

## Whoa! Visual Studio Code!

A whopping 50.7% of all respondents use Visual Studio Code for their [development environment](https://insights.stackoverflow.com/survey/2019#development-environments-and-tools). The next closest is the full Visual Studio at 31.5%.

![developer environments](/images/posts/stackoverflow2019/dev-environments.png)

When splitting out web, mobile and SRE/DevOps, the popularity of Visual Studio Code only increases, with mobile being the only category where it just barely doesn't hold the top spot (falling just behind Android Studio but, surprisingly, above XCode).

### Web tech still dominates

This probably shouldn't come as a huge surprise though, seeing as StackOverflow seems to be [dominated by JavaScript/front-end developers](https://insights.stackoverflow.com/survey/2019#technology-_-programming-scripting-and-markup-languages).

![most popular technologies](/images/posts/stackoverflow2019/technologies.png)

Still, web technologies still sit on the [bottom end of the pay scale](https://insights.stackoverflow.com/survey/2019#technology-_-what-languages-are-associated-with-the-highest-salaries-worldwide), particularly in the United States.

## Most Developers Are Employed By Small Businesses

Excluding self-employed individuals, a full 58.8% of developers on StackOverflow are [working at companies with less than 500 employees](https://insights.stackoverflow.com/survey/2019#work-_-company-size).

![company size](/images/posts/stackoverflow2019/company-size.png)

### And most like their jobs

Over 65% like their [current jobs](https://insights.stackoverflow.com/survey/2019#work-_-how-do-developers-feel-about-their-careers-and-jobs), at least slightly. Even a lot of those who don't necessarily like their current jobs, are still at least somewhat happy with their choice of career - nearly 3/4 of developers are happy with their choice of career.

![job satisfaction](/images/posts/stackoverflow2019/satisfied.png)

Perhaps they are so happy in their jobs because they are not (nor, largely, want to be) managers. 😉

![want to be managers](/images/posts/stackoverflow2019/managers.png)

## PHP Doesn't Pay

While Scala, Clojure and Go developers are [paid well regardless of their years of experience](https://insights.stackoverflow.com/survey/2019#work-_-salary-and-experience-by-language), PHP developers are paid the least (and seemingly by a lot) regardless of their experience.

![pay correlated to experience](/images/posts/stackoverflow2019/pay-experience.png)

Despite this, PHP still remains popular, being the [8th most popular language](https://insights.stackoverflow.com/survey/2019#technology-_-programming-scripting-and-markup-languages) at 26.4% of all respondents and still over 25% of professional developers.

## Developers Love Reddit

Social media is a key part of the roles I've had in DevRel, community management and marketing, so I was interested to see social media usage.

![social media](/images/posts/stackoverflow2019/social-media.png)

The differences between the all respondents and US respondents is pretty significant. Reddit still wins, by a lot more, but Twitter jumps from 5th to 2nd.

![social media in the US](/images/posts/stackoverflow2019/social-us.png)

A notable absence, though, is Twitch. Perhaps it wasn't included as an option on the survey, which is surprising given the popularity lately of live-coding streams.

## What Struck You?

What did you think of the survey? How does it compare to your experience, whether you are a StackOverflow user or not? I'd love to hear different perspectives.