---
layout: post
title: Getting Started with Offline Data in Web Apps Pt. 2
date: '2019-07-12'
description: Exploring what localStorage is, how it works and how it can be used to store and access data offline.
categories:
  - javascript
  - web development
comments: true
---

In this series of posts, I am looking at some options for dealing with data offline. The [first part](/blog/offline-data-pt1) explored options for determining if the user is offline or has a slow/poor connection. In this part, we'll looking at some options for storing data that we can access when the user is offline or even cache for those with a poor connection. Let's start by storing small(ish) amounts of relatively simple data and explore storing that using [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage).

## What is localStorage?

The best part of localStorage is that it is both easy to understand and easy to use. Basically, localStorage is an offline key/value store. The data, unlike `sessionStorage` which has an identical API, will remain saved across browser sessions. Thus it can be useful for accessing data when the user is offline.

It has some important limitations, however. For instance, it can only hold string values, but this does allow you to store serialized data. It is also [synchronous](https://www.quora.com/Is-localStorage-in-HTML5-always-synchronous). It only allows a storage quota of only about 5MB per domain (the exact amount can differ slightly depending on the browser).

> What happens if you exceed that quota? I couldn't find any recent articles on this topic, but [this article from Raymond Camden](https://www.raymondcamden.com/2015/04/14/blowing-up-localstorage-or-what-happens-when-you-exceed-quota) explored how each browser behaved somewhat differently.

There is no built-in data protection - any JavaScript code on the domain can access localStorage. In fact, you can simply open your browser tools and see all localStorage values in plain text. You can even edit any value via the console. This insecurity has led some people to suggest [not using localStorage at all](https://dev.to/rdegges/please-stop-using-local-storage-1i04).

Despite its limitations, localStorage can still be useful for storing simple values that maintain the state of an application when it is offline.

## Using localStorage

The API for localStorage is extremely simple. You set an item with `setItem()` and get an item with `getItem()`.

```javascript
localStorage.setItem('keyName', value);

let myData = localStorage.getItem('keyName');
```

You can also remove an individual item using `localStorage.removeItem('keyName')` or clear all localStorage for your domain using `localStorage.clear()`.

If you want to use localStorage to store something more complex than just a simple string, you'll need to serialize and deserialize the data.

```javascript
localStorage.setItem('complexData', JSON.stringify(data));
let complexData  = JSON.parse(localStorage.getItem('complexData'));
```

One other thing to mention is that you can listen for events on localStorage. This will return a `StorageEvent` that provides you details about the key that was modified and the old versus the new value. This won't work on the same page that is making the changes — it is really a way for other pages on the domain using the storage to sync with any changes that are made.

## Example

To give a simple example of all of these concepts at work, I create a CodePen that calls a remote API to populate a `<select>` list with types of drinks. Because this data is relatively small, I cache it in localStorage so that the list is populated even if the user is offline. If you select an item from the list, it will also store and keep that preference.

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="js,result" data-user="remotesynth-the-bold" data-slug-hash="PrLKPB" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="PrLKPB">
  <span>See the Pen <a href="https://codepen.io/remotesynth-the-bold/pen/PrLKPB/">
  PrLKPB</a> by Brian Rinaldi (<a href="https://codepen.io/remotesynth-the-bold">@remotesynth-the-bold</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

The demo is very simple at the moment, but, in a future iteration, I'll use this selection to pull more complex data from the API and use IndexedDb to store and retrieve this offline. As a sidenote, I feel almost guilty posting a demo this ugly on CodePen seeing all the amazing things folks create there. Saying that design is not my strong suit would be a serious understatement.

## Next Steps

We've seen that localStorage has a simple API that makes it easy to use to store certain types of data offline. As noted, it has some limitations, both from a functionality and security standpoint, that you need to be aware of. However, what if you need to store larger amounts of complex data offline? That's where we'll want to look at IndexedDb starting in the next part in this series.