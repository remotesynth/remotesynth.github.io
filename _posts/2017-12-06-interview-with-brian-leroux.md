---
layout: post
title: "From Cordova to Bots to Serverless - An Interview with Brian Leroux"
date: "2017-12-06"
categories:
    - general
description: Brian Leroux previews his upcoming presentation by discussing why he created arc.codes and why serverless matters.
comments: true
---

[![The Future of Development](/images/posts/Banner_The-Future-Of-Development.jpg)](https://certifiedfreshevents.com/events/future-of-development/)

[Brian Leroux](https://twitter.com/brianleroux) is one of the featured speakers at [The Future of Development](https://certifiedfreshevents.com/events/future-of-development/) online event that I am running next Friday, December 15 at 12pm ET. You can [sign up for free today](https://certifiedfreshevents.com/events/future-of-development/) .

Brian and I crossed paths when we both worked for Adobe - he was helping to lead PhoneGap and Apache Cordova, both of which fell under my areas of focus within my role at the time. A couple years later, we bumped into each other at PhoneGap Day in Salt Lake City and he told me about his new startup focused on bots, but recently he&#39;s gained a lot of attention for creating a tool called arc.codes for building serverless architectures. In this interview, Brian explains this journey and why serverless matter.

> **For those readers who may not know you, tell us a little about yourself and give us an overview of your technology/development background?**

Been writing code for a long time, but probably the first thing I did that got any significant attention was [wtfjs.com](https://wtfjs.com/) in 2007ish. A few years later, myself and a band of misfits created PhoneGap which was acquired by Adobe in 2011. From there I had the huge privilege of stewarding the opening moments of Apache Cordova. All that mobile work lead me to messaging, bots and -- a bit weirdly -- serverless.&nbsp;

> **What does your the current business you co-founded, Small Wins, focus on? What inspired you to create this business?**

Small Wins is our operating name which reflects a core belief in incrementalism. Our product is [begin.com](https://begin.com/) which is a tasking app for Slack. Somewhere around 2014 it was becoming clear that mobile had commodified, the winners were clearly Google and Apple and interestingly adoption via mobile apps had stalled. Mobile is still huge but there is no growth anymore. So the big question was: what are people doing with their attention on these devices? The answer is messaging. Slack was just starting to skyrocket in 2015 when my cofounder Ryan and I saw there was a window to shake up productivity if we got to work on messaging apps (sometimes called bots) right away.&nbsp;

> **How did working on bots lead you into the serverless space and to create [arc.codes](https://arc.codes/)?**

Yeah this was something I didn&#39;t expect to happen. I avoided it if anything. I was sort of done with the whole developer tooling space after close to a decade driving PhoneGap, PhoneGap/Build and Cordova. Don&#39;t get me wrong I loved it, but I was ready to dive into the consumer productivity and apps space with Ryan. It was around November of 2015. We had a greenfield in front of us. Choosing to build for the cloud is a no brainer. Choosing AWS is easily the lowest risk choice. Bots, real time NLP, conversational UI, and machine learning seemed risky enough! Faced with standing up our initial infrastructure it seemed really obvious that the puck was going towards this whole serverless / functions as a service model. You have to remember startups are risky af. Any edge we can get, anything at all, and we&#39;ll take it. API Gateway had *just* been released that July. I toyed with it a little and realized we could get zero downtime deploys to HTTP endpoints in &hellip; a few seconds. I had never seen anything like it. So we just went for it without much more thought.

At first, things where awesome but the team was small and we had less than a dozen endpoints. And remember automation tooling was completely non-existent. A thing called JAWS was out there but it wasn&#39;t any better than the Bash scripts we cobbled together. (Later that became Serverless&trade; the well known framework and venture-backed startup.) There was no CloudFormation support. There was no Terraform support. And worse, our method for development was, effectively, shitty scripts and checklists. Inevitably, and unsurprisingly in hindsight, it began to fall apart. We didn&#39;t know what we had deployed where. We had bugs that were nearly impossible to trace, let alone reproduce and fix.

We had to automate our infrastructure provisioning and deployment because we were getting into deep trouble. We created a manifest format .arc as a nod to other UNIX-y config manifests like .bashrc or .vimrc. Initially the format stood for Amazon Run Commands though today I&#39;d say Architecture Run Commands.

We automated against the .arc manifest with npm scripts. Things rapidly became predictable. Our cadence improved drastically. Our quality and speed to resolution followed. Other approaches started to get attention and we felt we had a better answer. A lot of frameworks out there are being built with the goal of being a framework. We built .arc to build a product and it shows. It is designed for standing up web and Slack apps rapidly with both staging and production environments pre-baked. Provisioning takes minutes. Deployment is measured in seconds.

So I don&#39;t believe cloud infrastructure projects make good products and I also believe, quite strongly, that proprietary code that isn&#39;t our core product is a liability not an asset. Open code is faster code. Many eyeballs do make all bugs shallow and it&#39;s a great quality forcing function from a performance and security perspective. Ryan and I debated it a bunch and I kind of couldn&#39;t believe I was going to do this again but it was the best idea for the company so we spoke with the JS Foundation and donated the code and copyright to them to ensure that the code was open source and so was the governance. We announced it in July of 2017 at Node Summit as JSF Architect though colloquially we mostly call it &#39;arc&#39;.

> **To many people, serverless seems like just a buzzword. Why do you think it is important for developers to learn about it? What kind of impact do you think it will have on the future of development?**

It is a buzzword! The idea of entirely managed infrastructure is obviously not super new but the idea of removing the *server* metaphor is. This is very new and a super powerful evolution on microservices. Systems built this way are anti-fragile in ways I&#39;ve never seen with theoretical infinite availability. Its seriously hard to bring down a system when every endpoint is deployed independently. Deployments, with zero downtime, are measured in seconds which means you get more iterations. More iterations means you get an edge (possibly) finding product/market fit. *You learn faster.* The pricing is also nice. 10 Million executions is $1 a month.

Ultimately being faster and more resilient is the part that makes me excited as a developer.

As to impact, I have no idea but there is a fun thought experiment that this level of managed infrastructure could lead the first solo employee billion dollar startup. I like the ambition in that idea. With legacy techniques a solo employee billion dollar company is most definitely not unattainable.

> **Your presentation says that arc.codes is serverless on &quot;easy mode&quot; - without giving away the whole presentation, can you explain what you mean by that?**

JSF Architect shines in its focus on creating fast iterations. Anyone with an AWS account and a text editor can spin up an endpoint in a few minutes. In another 20 you can have a custom domain name propagated complete with a fully scalable backend. So that&#39;s what we&#39;ll do.

[Sign up for The Future of Development for free!](https://certifiedfreshevents.com/events/future-of-development/)