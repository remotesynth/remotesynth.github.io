---
layout: post
title: "Can Machine Learning Potentially Stop Internet Trolls?"
date: "2017-02-27"
categories:
    - general
description: A Google company has been working on an anti-trolling API.
comments: true
---

Last week, a new project named the [Perspective API](https://www.perspectiveapi.com/) was opened to the public by Jigsaw (which is apparently supported by Google). Perspective uses a toxicity scale to try to determine how similar any given text is to other text that people rated as toxic. Details on exactly how they recruited people to help perform these initial ratings isn't completely clear (according to [this article](http://www.theverge.com/2017/2/23/14713496/google-jigsaw-perspective-software-ai-machine-learning-developers), they presented them to panels of 10 people at a time for feedback), but there is a built-in learning aspect to the ratings (at least as demoed in the writing experiment on the site).

Perspective is currently beginning to roll out API access over the course of the year to developers who submit a request.

In simple tests conducted by [The Verge](http://www.theverge.com/2017/2/23/14713496/google-jigsaw-perspective-software-ai-machine-learning-developers) and [Mashable](http://mashable.com/2017/02/23/google-jigsaw-moderation-tool/), the results seemed mixed. These anecdotal tests combined with the experiments made available on the site, seem to indicate that the algorithm is very good at identifying obviously trollish behavior (especially when profanity is involved), but less effective against text that is less blatant.

Here's an example:

![](/images/posts/perspective.png)

The items in each column are ranked by toxicity, with items showing a square having moderate to moderately-high toxicity (I am filtering out the more highly toxic items in this image).  On the left hand column, it seems odd that "Dreadful: I'm a Remainer" is considered slightly more toxic than "left wing wimps" for instance. On the right hand column, the comment about xenophobia and racism seems to be strangely overrated. Even the comment above doesn't truly seem (to my eyes) much more toxic than the last comment on the bottom of the right-hand column, which the algorithm rated as not toxic (sure, the word cowards could have been a trigger of sorts, but isn't necessarily toxic depending on the context, which is obviously not entirely clear here).

So clearly, this isn't ready to be a fully automated tool yet, but it could help companies at least begin to identify and intervene with potentially abusive online behavior. Even if that would still require manual intevention, perhaps, with some refinement this tool integrated into some sites (hello, Twitter, Reddit and Hacker News!) could help raise red flags for moderators to intervene. However, if this is to be more widely used, I think there would have to be more openness as to how scores are calculated and the makeup of the panels (perhaps this is being done already and it's simply not obvious to me or open to only those with API access) - the last thing we need is to create a means of easy censorship.

