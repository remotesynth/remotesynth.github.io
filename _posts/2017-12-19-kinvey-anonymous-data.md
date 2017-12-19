---
layout: post
title: "Getting Started with Kinvey mBaaS - Pulling Data Anonymously"
date: "2017-12-19"
categories:
    - Kinvey
description: The very first step to getting started with the Kinvey mBaaS
comments: true
---

In my new role at work I'm going to be focusing on [Kinvey](https://www.kinvey.com/). Much of this is as new to me right now as it may be to you as well, so I invite you to join me in this series of posts (of which this is the first) where I'll be experimenting and learning Kinvey (along with some other technologies).

For those of you who haven't heard of Kinvey, it is an [mBaaS](https://en.wikipedia.org/wiki/Mobile_backend_as_a_service) but has a ton of features over and above your typical mBaaS. Nonetheless, one of the first things you'd typically want to do is just pull some data from the data store. In this post, I'll explore how this works in Kinvey and how you might implement this in a simple JavaScript application.

## Getting Set Up

To get started, I created a new app in the Kinvey console. Since I am going to try to pull data, I created a collection. Collections can either use the Kinvey data store or a data service that can connect to any number of sources (REST, Salesforce, SQL Server, etc.). For the sake of this demo, I just used the Kinvey Datastore.

![choosing the Kinvey data store](/images/posts/datastore.jpg)

For anyone familiar with NoSQL datam stores, the Kinvey data store should look familiar (it's just MongoDB in the background).

![My sample data](/images/posts/data.jpg)

> As someone mildly obsessed with The Legend of Zelda: Breath of the Wild and also as a completionist, I decided to try to build an app that lists all the shrines in Zelda, where to find them and (eventually) allows me to check them off. If you aren't a Zelda fan, the important thing for the sake of this post is simply that I have pre-populated the data in a collection so that I have something to pull.

Once the data was set, it's time to pull it down.

## Getting Data with the JavaScript (aka HTML5) SDK

For this simple example, I just pulled the data into straight JavaScript and HTML. To do this, I used Kinvey's [HTML5 SDK](https://devcenter.kinvey.com/html5/downloads).

> A note about SDKs: While Kinvey offers a REST API, they also include a number of SDKs for different platforms and frameworks such as Angular, Node, native iOS and Android and many more. You get a number of benefits when using the SDK over the REST API, including things like local caching and syncing, at no extra cost.

The simple code for the sample is below. Let's take a look and then go through it.

<script async src="//jsfiddle.net/remotesynth/kj1w9r2L/2/embed/js,html,result/"></script>

Overall, the code is pretty simple. There's just one thing that makes getting anonymous data somewhat unique in Kinvey...

![users everywhere](/images/posts/user.jpg)

### Creating an Implicit User Account

...there is still a user - even when I am getting the data "anonymously."

Kinvey uses a concept of [explicit versus implicit users](https://devcenter.kinvey.com/html5/guides/users#ExplicitvsImplicit). An explicit user would utilize one of the various built-in authentication methods Kinvey offers (or a custom one) while an implicit user is auto-generated. The case above is an implicit user and the generated user record looks something like this:

![The auto-generated user in my users table](/images/posts/implicit_user.jpg)

The way the app is handling the user, every new, unique connection will create a new implicit user. So, if I open this on my desktop browser it will create a new, random user account. If I then open it on my phone browser, it will create another new, random user account. Yes, there will be lots of auto-generated users, and that's ok.

However, subsequent connections from the same device or browser are cached. This is why the code only calls the `signup()` method if the active user (`activeUser`) is not already defined.

This caching can be seen in effect by viewing your browser's local storage and finding the active user as shown below.

![The cached active user](/images/posts/activeuser.jpg)

Suffice it to say, if I wanted to test the auto-login process, I'd simply remove that key from local storage and the login will be re-triggered.

### Getting the Data

Now that I am logged in (anonymously), I can get data. First, I connect to the data store that I want to pull from (the list of Zelda shrines) and pull the data:

```javascript
var dataStore = Kinvey.DataStore.collection('shrines');
dataStore.pull()
	.then(function(regions) {
    	// ..
    })
    .catch(function(error) {
    	console.log(error);
    })
```
That part is pretty easy and straightforward. However, one thing I want to point out is that, since I am using the SDK, we can see the data has been cached locally automatically.

![The WebSQL Cache](/images/posts/cache.jpg)

## Next Steps

I know I wrote a lot here just to get some data, but understanding that you need to have a user in _all cases_ for Kinvey was a little bit of a mental hurdle for me at first. In the next post, I'll look at how I did the same thing, but in a Vue.js application, which presented its own small, unique challenges.