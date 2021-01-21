---
layout: post
title: Thinking in Jamstack
date: '2021-01-21'
description: One of the more difficult things a new Jamstack developer can face is a change in mind set about when to render content.
categories:
  - Jamstack
comments: true
---

I feel like one of the difficulties that many developers face when considering adopting the Jamstack is that it requires a change in your mental model of how to build an application. This often results in a potentially misapplied belief that Jamstack is just for building simple applications. You'll hear comments along the lines of a comment on my [recent post](https://dev.to/remotesynth/what-is-the-jamstack-in-2021-1p1n):

> I'm sure static sites are awesome when building a site but most of what I build is a webapp that requires a lot of dynamic info.

The thing is, Jamstack is all about building sites with a lot of dynamic info! But it also requires you to retrain your brain a bit. In this post, I want to share how I like to think about it in the hopes that it might potentially help others get over that mental hurdle.

> On a side note, if you're interested Jamstack, make sure to join me and 20 amazing speakers at [TheJam.dev](https://thejam.dev/), a Jamstack community conference being held on January 28-29.

## The Traditional Server-side Application Model

I'm going to age myself here but, having worked for decades building these types of applications, they were really easy to understand. Essentially everything happened on the server side (usually within an application server like PHP, for example). The user would interact with the web application, which would make a request to the server. The server would parse this request and then assemble the page, which meant the entire HTML/CSS/JavaScript, and send back the response which would then render for the user in the browser.

What we called Web 2.0 in the early days made some changes to this process, but, in many cases, it was cosmetic. The asynchronous JavaScript call would still make a request to the application server. This might send back XML or, in many cases, it would still send back a rendered HTML snippet.

The important point here is that there was never a need for a developer to give much thought about when to access data. It was always just accessed on the server following a request. Whether populating the content of a blog post or the user's account details, it all happened the same way.

## The Modern SPA Application Model

The SPA model changed this quite a bit. The application was no longer sending the full HTML/CSS/JavaScript of a page to the client. Instead, it sends an application shell that the application lived in, made of HTML/CSS/JavaScript, and would populate the content and data on a page via a series of API requests to the backend. This backend was not typically monolithic as in the case of the traditional model, but instead each API call could be using my own API on a server (perhaps using Node though not necessarily), a service running as a cloud function, a third-party API, etc.

In this case, what was returned was JSON data rather than rendered output. While developers were now making all kinds of client-side calls to these various backends, the mental model was still fairly simple. The data that populated a page was generally loaded on the client in response to an asynchronous request, though you may choose render some complex or sensitive pieces on the server. However, even when something was rendered on the server, it was in response to an asynchronous request.

## The Jamstack Model

The reason both of these two models remain easy to grasp is that it always follows a "client requests x => application gets x and returns it to the user." A developer doesn't need to think about _when_ it makes sense to get something as it is always in response to a specific request. One might think that, since it is dependent on APIs, that the Jamstack model and the SPA model would be essentially the same, but, in my opinion, pre-rendering changes the entire mental model. Pre-rendering content is about much more than just loading some Markdown files and determining what to pre-render and what not to takes some thought.

There are two points in time that you can integrate dynamic content into a Jamsack application, and when each is appropriate may differ across pages or even in different parts of a single page:

* **Build time** - A Jamstack application may load data from files, APIs, third-party services or even a database at build time. If you're used to the SPA model this may seem like just a place for the application shell plus long form content from Markdown files, but it can be much more than that. Already it has become common for Jamstack applications to use headless CMS and headless ecommerce systems to populate content or product listings at build time. However, this is relevant for any content from any API that a) applies to all users and b) persists for a substantive amount of time (what is "substantive" is kind of flexible, and costs may factor into it as it impacts your monthly build time). You can think of it like a content cache that applies to all your site's users. Parts of the cache may need to be refreshed at specific intervals - that could be once a month, once a day or even multiple times a day dependent on the type of content. For example, if I'm building a site about Orlando, where I live, I might want to include the daily local weather forecast. I _could_ call that on the client, but it would be more efficient to simply call it at build time and update the build each day to refresh it. 
* **Run time** - This is similar to an SPA whereby the Jamstack application calls an API that returns JSON from the client using JavaScript and populates the page content in the browser. This should typically be content that is user specific, needs to update frequently, or is in response to a specific user action. For example, an ecommerce site may have product details populated at build time, but things like the current inventory, shipping options/prices based upon the user's location, or the user's shopping cart would all be populated at run time in the browser. As you may notice, in this example, the content on a single page (product details) may be a combination of both pre-rendered (build time) content (i.e. the product name, photo and description) and run time content (i.e. the product inventory and shipping options based on location).

To further complicate things, new tools like Next.js allow the addition of a third option, which is SSR for specific routes, but if you're building a "static first" Jamstack site, that should be the exception rather than the rule. The addition of things like [Netlify Edge Handlers](https://css-tricks.com/netlify-edge-handlers-2/) make the story even more complex from a mental model perpective, but the end result of all of these changes is that a Jamstack site can be incredibly dynamic - it's just a matter of determining *when* that dynamic content needs to be rendered.

## Wrapping Up
The point here is that dynamic data isn't just a client-side thing in a Jamstack application and Jamstack developers need to think about each piece of content/data in terms of when it should be retrieved and rendered. I think Cassidy Williams summed this up much more succintly in a recent tweet:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I admit personally I didn&#39;t really &quot;get&quot; what the big deal was about Jamstack until I started thinking of it this way. Data really can be pulled in whenever, it&#39;s more about the decoupling/separation of concerns.</p>&mdash; Cassidy (@cassidoo) <a href="https://twitter.com/cassidoo/status/1351590001675563008?ref_src=twsrc%5Etfw">January 19, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

The key word there is _whenever_. Without taking into account things like SSR and edge handlers, to me, the critical distinction in thinking about "whenever" when it comes to a Jamstack app is determining whether that data should be pulled  _whenever the site is run_ or  _whenever the site is built_.




