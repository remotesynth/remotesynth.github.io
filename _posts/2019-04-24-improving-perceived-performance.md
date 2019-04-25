---
layout: post
title: "Promoting Perceived Performance with Prefetching"
date: "2019-04-24"
categories:
    - web development
description: A look at two libraries designed to help improve the perceived performance of web apps
comments: true
---

There will always be a difference between how your site actually performs versus how people perceive it to be performing. This perceived performance is impacted by any number of factors, some of which you have no control over, from network or connection speed to simply differing user expectations. Actual site performance is something you largely have control over as a developer, but how your site is perceived to be performing by the end user is, for the most part, beyond your control.

That's why some new projects fascinate me. They attempt to improve that perceived performance by the end user by using different methods to prefetch the content they may load to allow it to load _before_ they want it.

In this post, I want to take a look at two libraries: [quicklink]() and [instant.page](). Both attempt to utilize the `<link rel="prefetch>` feature to load pages. This feature is relatively new and isn't supported across the board, as you can see in the support matrix from [caniuse.com](https://caniuse.com/#feat=link-rel-prefetch).

![prefetch support](/images/posts/prefetch/prefetch-support.png)

> Learn all about `preload`, `prefetch`, `preceonnect` and other types of `<link rel>` tags in [this excellent post by Ivan Akulov](https://3perf.com/blog/link-rels/).

## quicklink

[Quicklink](https://github.com/GoogleChromeLabs/quicklink) is a project from Google Chrome Labs. It is designed to prefetch any links that are in the viewport to speed up subsequent page loads. It does this by relying on two newer browser APIs: [Intersection Observer](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) and [requestIdleCallback](https://developer.mozilla.org/en-US/docs/Web/API/Window/requestIdleCallback).

These new APIs are not universally supported, meaning that you have to use one or more polyfills (depending on which browsers you need to support), otherwise support is limited to Chrome, Firefox, Edge, Opera, Android Browser, Samsung Internet.

Let's take a quick look at how to use it in a simple web page. The basic example is as simple as calling `quicklink()` after the page loads by either adding a listener for the load event or just putting the `<script>` tag before the closing body tag.

```javascript
window.addEventListener('load', () =>{
	quicklink();
});
```

You won't get any notification that the content has loaded, but you should immediately notice some improvement in the load time of links you click.

There are also a bunch of customization options. By default the library uses XHR to load all the links but you can ask it to use the fetch API and fall back on XHR:

```javascript
quicklink({ priority: true});
```

You can also specify what URLs it should prefetch in case you want to limit how much it attempts to prefetch (which is basically anything within the current viewport). For instance, you can specify an DOM element containing URLs to prefetch.

```javascript
const nav = document.getElementById('menu');
quicklink({ el: nav });
```

You can also specify a custom array of URLs to prefetch or even a pattern of URLs to ignore.

It is important to note that, by default, this only loads content for current origin (i.e. same URL). This is because unless the others have [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) enabled, you'll hit a cross-origin security issue. This is true whether you specify a list of URLs or whether you use fetch or XHR.

To override this behavior you can specify a list of allowed origins or you can allow all origins.

```javascript
quicklink({origins: true});
```

However, allowing all can result in a long list of cross-origin scripting errors that you probably want to avoid as seen below (this is testing locally on a simple site I created for the purpose).

![cross origin errors](/images/posts/prefetch/cross-origin-issues.png)

All in all, the library is easy to use, and even accepting the browser compatibility issues, it can be a very easy progressive enhancement to improve perceived performance on browsers that will support it.

## instant.page

[instant.page](https://instant.page/) takes a different approach to solving the same problem. Rather than load everything in the viewport, it looks at content that the user is in the process of hovering or clicking and then starts prefetching that content. This prevents the issue of preloading too much and instead focuses on preloading only that content the user is likely to click.

This change in approach also affects the technical implementation. instant.page does not rely on `IntersectionObserver` or `requestIdleCallback` because it only prefetches items based on the `touchStart` or `mouseover` events. However, it does still rely on `<link rel="prefetch">` which is not supported in Safari or Edge at the moment. For this reason, it is designed as a progressive enhancement as well, meaning it will improve the experience where it is supported but not hurt it where it isn't.

Using instant.page is simply a matter of including it.

```markup
<script src="//instant.page/1.2.2" type="module" integrity="sha384-2xV8M5griQmzyiY3CDqh1dn4z3llDVqZDqzjzcY+jCBCk/a5fXJmuZ/40JJAPeoU"></script>
```
There are fewer configurations for instant.page than quicklink, but there are some. For instance, as with quicklink, external links are not preloaded by default, however adding `data-instant-allow-external-links` to the body tag will automatically attempt to preload links from any URL or you can specify specific URLs by adding a `data-instant` attribute to them. Interestingly, in my local sample this didn't generate cross-origin scripting errors. In the below recording, the only failed load you can see in the network tab is a page that specifically doesn't exist for testing purposes.

![loading external domains](/images/posts/prefetch/prefetch-instantpage-opt.gif)

I think this is just a difference in implementation rather than function as the pages do not load noticeably quicker and similar tests with quicklink also showed up in the network tab in a similar manner but did trigger the console error.

There are also similar attributes to customize other behavior such as allowing pages with a query string to be prefetched, which they are not by default (as some may trigger an action) or to specify a link specifically not be loaded. 

## Does it help?

Testing perceived performance is a difficult task. Exactly how much better the performance seems depends on a large number of factors including the user's connection speed, the site's load times, and more. It can be something that is difficult to measure exactly. My local demo doesn't do the technique justice since everything locally loads quickly and the demo itself was relatively simple - so even on external hosting the perceivable difference might be minimal. The limitation of loading large external sites this way without CORS enabled adds to the difficulty in testing and measuring.

The Google Chrome Labs team behind quicklink themselves acknowledge this problem. They created a more complex example and found that quicklink could improve page-load performance by up to 4 seconds, as they demonstrate in [this video](https://www.youtube.com/watch?v=rQ75YEbJicw&feature=youtu.be). That would be dramatic, but your mileage may vary.

That being said, both libraries are remarkably easy to implement and carry few drawbacks that I could identify, so it would seem there is little harm in utilizing them - even a small improvement in the perceived performance by your users could have a big beneficial impact.