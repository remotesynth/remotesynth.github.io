---
layout: post
title: Getting Started with Offline Data in Web Apps Pt. 1
date: '2019-06-28'
description: Different options for determining the user's online/offline status and connection speed.
categories:
  - javascript
  - web development
comments: true
---

It is a growing expectation of a modern web app that it should work offline in one manner or another. In fact, offline availability is a key part of a PWA. If your application relies on some form of data, which most do, this can be complicated.

In this series of posts, I want to take a look at some options for dealing with data offline. A key part of that will be working with things like [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) and [IndexedDb](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API). However, an important step to determining whether to use online or offline data is knowing whether your application is currently online or offline. In this first post in the series, I'll look at some very simple web APIs that help you in this regard.

## Navigator.onLine

The goal of [Navigator.onLine](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorOnLine/onLine) is very basic - it just returns the online status of the browser as `true` or `false`. It pretty much works as advertised.

![navigator.onLine](/images/posts/navigator_online.gif)

This will work across browsers on mobile and desktop, except Opera.

There are two ways to utilize this. The first is simply in a conditional like:

```
if (navigator.onLine) {
	\\ call my external API for data
}
```

The second way would be to respond to changes in the online status of the user by adding an event listener.

![navigator.onLine](/images/posts/navigator_online2.gif)

## Network Information API

While `Navigator.onLine` works well, it doesn't give you any details about the user's connection other than whether it is online or offline. For instance, what if the user's connection is extremely slow? In this case, you might want to rely first on some sort of local data that is refreshed by remote data as it becomes available or, depending on the nature of the remote data, not even bother with the remote call at all.

In theory, this is what the [Network Information API](https://developer.mozilla.org/en-US/docs/Web/API/Network_Information_API) provides - not just the connection status, but critical details about the connection. What's the problem then? It only works in Chrome (on desktop and Android) and Opera currently.

To see how this works, I created a [simple jsFiddle](https://jsfiddle.net/remotesynth/axywLu18/16/). If you are on Chrome, open your Chrome Developer Tools to the "Network" tab and then change the throttling drop down (which should read "no throttling" to a different preset such as "Fast 3G", "Slow 3G" or set it as "offline."

<script async src="//jsfiddle.net/remotesynth/axywLu18/15/embed/js,result/"></script>

One interesting thing to note is that, when "offline", the connection type in my tests still read "4G" but the `rtt` and `downlink` were all zero. This might lead you to ask, what do each of these values even mean?

* `effectiveType` - The type of connection being one of the four values of 'slow-2g', '2g', '3g', or '4g'.
* `rtt` - This stands for "round trip time." This is the "time it takes for a packet to go from the sending endpoint to the receiving endpoint and back." ([source](https://www.callstats.io/blog/what-is-round-trip-time-and-how-does-it-relate-to-network-latency))
* `downlink` - This value is an estimate of the bandwidth in megabits per second.
* `saveData` - This value indicates whether the user has enabled some kind of reduced data usage option.

The Network Information API could be potentially useful for determining when to rely upon remote data versus local data if it was more broadly adopted.

## Next Steps

In this post we took a look at tools to determine whether the user's internet connection allows us to reliably get data from a remote source versus local data. In the next post in this series, I'll start to look at some ways to store data locally using localStorage and then, in a subsequent posts, IndexedDb and tools that can help.