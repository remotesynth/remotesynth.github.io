---
layout: post
title: Is JAMstack All Branding and Little Substance?
date: '2020-02-18'
description: Is the JAMstack just fancy buzzword marketing or is there actual substance behind the term? I share my thoughts. 
categories:
  - JAMstack
comments: true
---

Last week, when asked for to share a contrarian position, Nicole Sullivan posted something that drew a lot of people's attention:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">JAMStack is 99.9% branding and .1% substance. 😳😆 <a href="https://t.co/nxoEVQ43oE">https://t.co/nxoEVQ43oE</a></p>&mdash; Nicole Sullivan (@stubbornella) <a href="https://twitter.com/stubbornella/status/1226365361722773508?ref_src=twsrc%5Etfw">February 9, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Needless to say, the people who love to hate JAMstack loved it and the rest of us (who love to love JAMstack I suppose) were more than a bit put off.

The thing is, Nicole is not entirely wrong. The JAMstack term was, in fact, all about branding. It was created by the folks at Netlify in 2016 as a way of rebranding what, until then, we'd called "static sites." We've seen enough of this kind of rebranding before in the developer ecosystem to be skeptical - such as when Netscape famously changed the name of LiveScript to JavaScript in order to capitalize on branding opportunities with Sun's Java despite the lack of any real-world connection between the two. But, I'd argue that in the case of static sites to JAMstack, the goal wasn't to manipulate developers with empty marketing jargon, but to make the name _more_ appropriate to the solution.

## What's Wrong with Static Sites?

We still call tools like Hugo or Gatsby static site generators, so why would the end result of the process not be a "static site"?

The truth is that for a long time, they were by and large _static sites_. When I wrote my Static Site Generators report for O'Reilly back in 2015, I listed 3 criteria for determining if your site was a good candidate for being a static site:

1. Focus on Delivering Content - static site generators at the time were heavily focused on creating and delivering long form content (usually written in Markdown) and that's what they were optimized for.
2. Low Degree of User Interactivity - sure APIs existed at the time, but adding something like a login or a shopping cart to a static site was complex and, largely, the services to support that didn't yet exist or were in their infancy.
3. Update Infrequently - building and deploying these sites was cumbersome and slow. Services like Netlify were new, so a the time most were deployed via FTP.

As you can see, these do not apply in any way to the modern JAMstack. That's because static sites described only an end result (static files) and JAMstack is about a way of building sites that, while deployed as static files, are far, far from static either in the build process or in the end result.

## Why People Love to Hate the Name JAMstack

First of all, developers love to hate so-called buzzwords even as we proliferate their existence. Think about the fact that you can't use the term serverless without addressing the complaint that there are servers involved (do you know a developer who is unaware that serverless code runs on actual server somewhere?). We talk about IoT, VR/AR (or even XR), DevOps, DesignOps, continuous deployment...the list goes on. For a group that professes to hate buzzwords, we sure do love to use them. And for all our complaints, no one typically has a better, non-buzzword name for things anyway. (Even if they did, wouldn't that thereby be the new buzzword in the end?)

So part of it is generic buzzword hate. The other part is based on a legitimate complaint: JavaScript, APIs and markup (the JAM in JAMstack) can describe pretty much every site on the web. Overly generic sounding buzzwords immediately set off most developer's BS detector.

My answer is twofold:

1. Despite the acronym, JAMstack is more about [how you build your site](https://remotesynthesis.com/blog/m-is-for-markup) not the ingredients of it. Or, as Divya said in her post [What makes a site JAMstack?](https://dev.to/shortdiv/what-makes-a-site-jamstack-ib1):
	> The JAMstack is a methodology rather than an outcome. You could say that a JAMstack site is a static site but a static site is not necessarily a JAMstack one.
2. I don't have a better name suggestion. I didn't back in 2016 when Netlify first shared the name with me, and I still don't. Do you?

## Is there Substance to the JAMstack?

Up to this point, we've covered why a rebranding was necessary for "static sites" and some of the issues people have with the JAMstack name, but back to Nicole's original case that there is no substance to it. Three (or so) years ago, you could make the case since the reality of static sites hadn't changed with the move to JAMstack, even if the rebrand was necessary to counteract people's misconceptions. However, so much has happened in those three years and so much new ecosystem exists around the architecture, that I do not agree that the name is just marketing.

Today's JAMstack ecosystem isn't just about static site generators mixed with some serverless functions and API calls. There are companies and tools built specifically for addressing this architecture, from adding registration/authentication, to enabling ecommerce and shopping carts, to allowing inline creating/editing of content for non-technical content creators. So much has changed in those few years that, in looking to update our O'Reilly book "Working with Static Sites", Ray and I determined it would be basically a complete rewrite.

Yes, JAMstack still sounds perhaps too vague and all-encompassing. It's an imperfect term that can be justifiably called marketing, but it still describes something important that should not be dismissed.