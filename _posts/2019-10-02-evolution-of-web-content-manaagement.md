---
layout: post
title: The Evolution of Web Content Management
date: '2019-10-02'
description: A look at the evolution of web content management from the early days of the web to the headless, cloud-based CMS systems of today.
categories:
  - web development
  - static sites
comments: true
---

If we built this city on rock an' roll (and my sources on this are as incontrovertible as Starship and Mannequin 2: On The Move), then we built this web on content. HTML was one of the foundational technologies behind the web from day one and it is essentially a means of formatting documents to be served on the internet. Documents, of course, are of no more value than the content they contain.

Today, we like to talk a lot about building web applications, but content is still the foundation to the majority of the web. Managing that content in the early days was simple, but, since then, the tools we use to create and manage content across the web have evolved to a degree that they have almost come full circle. In this post, I want to look at the evolution of web content management from the early days of the web to the headless, cloud-based CMS systems of today.

## Early Web Content Management

The early web was static pages. Editing the content required understanding the markup (HTML) and formatting content for display on the web. For simple documents this wasn't too difficult as early HTML was fairly simple (CSS, while it existed, wasn't broadly adopted by browsers until around 2000).

This simplicity was powerful, however, as it meant that anyone could create and maintain web content with a minimal amount of training. Obviously, as web sites became larger and with more complex designs and user interfaces, this became more complex. Some tools like Dreamweaver started supporting templates to make it easier to add content within repeatable design elements, but this required a whole level of development expertise that the average content creator did not possess.

![Dreamweaver Templates](/images/posts/webcms/dw_templates.gif)<br>
_Source: [DWFAQ.com](http://www.dwfaq.com/Tutorials/Basics/dwtemplates1.asp)_

## Welcome the CMS

Early tools like ColdFusion, Active Server Pages, PHP and server side includes arrived in the mid-to-late 90s and with them came the ability to serve dynamic content from a database. Many companies developed proprietary web content management tools, such as AOL reportedly [as early as 1992](https://www.quora.com/When-was-the-first-web-content-management-system-CMS-released). The late 90s saw the release of some of the first content management systems (CMS) appearing on the market.

[Vignette's StoryServer](https://en.wikipedia.org/wiki/Vignette_Corporation), most commonly cited as the first commercial CMS, was released in 1997. The early goals of these tools was twofold:

* Allow the ability of non-technical content creators to create and edit content across large web sites.
* Create a content workflow that allowed a typical editing and approval process that existed on other publishing platforms.

Those initial goals may seem simple, but the needs of large sites became increasingly complex, with internationalization, complex navigational structures and very specific length and layout requirements for content blocks. Subsequently, these tools became incredibly complex and expensive.

## Rise of Open Source

Expensive, complex and proprietary enterprise CMS systems were not a workable solution for many sites and businesses. At the same time, in the early 2000s, the open source movement was on the rise. This helped drive the development of open source content management solution like Drupal in 2000, Joomla in 2005 and, of course, Wordpress in 2003.

All of these are still the most widely used solutions today. All three combined make up about 70% of all CMS usage according [current statistics from 2019](](https://w3techs.com/technologies/history_overview/content_management/all)). Wordpress is used by "33.6% of the top 10 million websites as of April 2019" and usage appears to be rising.

![CMS usage statistics](/images/posts/webcms/cms_usage.png)<br>
_Source: [w3techs.com](https://w3techs.com/technologies/overview/content_management/all/)_

The problem with these tools for some was that they could be difficult to host and maintain for multiple reasons. First, they required servers or hosting that supported the language (PHP for Wordpress, for instance) and the necessary database servers. Like their enterprise CMS counterparts, customization required required developers with a depth of knowledge of both the language and the tooling and tags required to build front-ends specific to the tool. Plus by their sheer popularity, they became a target and, thus, a potential security risk, especially for companies that didn't have the wherewithal to actively patch or secure their installations. Finally, Wordpress in particular has been accused of growing unwieldy and bloated in the long run due to an overwhelming number of plugins.

![Wordpress Plugins Meme](/images/posts/webcms/wp_plugins.jpg)

## Little Fluffy Clouds

The late 2000s and early 2010s saw the rise of web-based services like Wordpress.com, Squarespace and Wix that essentially enabled companies to move their site hosting to the "cloud." This eliminated the problems of having to build and maintain servers to host and run their CMS implementation but also effectively outsourced the security concerns. Their install was always the latest version and always patched with any security update.

![You all get a cloud](/images/posts/webcms/youallgetacloud.jpg)

These are good solutions for any number of sites and, in particular, smaller businesses. They provide an easy solution with minimal setup and no real need for development expertise, while still offering a reasonable amount of customization. What they often lack is the ability for anything beyond basic customization that might make them suitable for more complex sites.

These web based tools did have a big thing in common with their open source brethren and even most enterprise CMS at the time - a tight coupling of the front end of the site with the back end.

## What the Heck is Headless?

This tight coupling posed a problem in the early 2010s as smart phones were becoming ubiquitous. This necessitated not only new paradigms of web development like responsive web design but also meant that content may be used for both a web site and a mobile app. Over the subsequent decade (almost) we've seen a continuing proliferation of devices that complicate the thinking around where and how our content is being published.

At the same time, we were beginning to see the rise of services such softw-are-as-a-service (Saas), platform-as-a-service (PaaS), backend-as-a-service (BaaS)...

![Say x as a service one more time](/images/posts/webcms/as_a_service.jpg)

A headless CMS is essentially the back end of a CMS "as a service." It decouples the front-end display of content from the back-end creation and management of that content. Instead of using proprietary tags to create the front-end, a developer would just have to call the headless CMS API.

Most of the popular examples of this are cloud-based services like [Contentful](https://www.contentful.com/), [Forestry](https://forestry.io/), [Sanity](https://www.sanity.io/) and others. However, many enterprise and open-source CMS solutions have also adopted the headless approach. In theory, even Wordpress is capable of functioning this way using its REST API.

## And the Circle is Complete

![the circle is now complete](/images/posts/webcms/circle_complete.gif)

The early 2010s also saw the start of tools like [Jekyll](https://jekyllrb.com/), [Middleman](https://middlemanapp.com/), [Hugo](https://gohugo.io/) and other so-called "static site generators". These tools took markup (often in Markdown combined with templating tools) along with HTML, JavaScript and CSS (often using preprocessors like Sass) and generated a static web site.

Originally, these tools were adopted largely by developers for things like blogs or, especially when [GitHub Pages added support for Jekyll](https://help.github.com/en/articles/setting-up-a-github-pages-site-with-jekyll), project sites. The tooling was such that it wasn't easy for a non-developer to use these tools since they required comfort with the command-line, editing raw markup and often complicated deployment. There was also limited support for even simple dynamic elements like a contact form without resorting to third-party embeds.

Things started to change with [Netlify](https://www.netlify.com/) and other services that first simplified the deployment process and then built the tooling and services required to turn these "static sites" into something far more dynamic - the [JAMStack](https://jamstack.org/).

But, tie the JAMStack into a headless CMS and you end up with the best of both worlds. You get the comfort simplicity of the old web in terms of content creation - similar to static templates before enterprise CMS systems complicated front-end development - with the comfort of the content editing experience that non-technical content creators and editors need. Plus you get the usual benefits of JAMStack such as improved speed and security.

## What's Next?

The next step is simplifying the process of developing JAMStack sites that are tied to content sources (a headless CMS, an API, or any of a number of data sources). Some part of this already started with tools like [NetlifyCMS](https://www.netlifycms.org/) - which has a one click deploy of a CMS-backed JAMStack site - and has continued with services like [Stackbit](https://www.stackbit.com/) - which allows you to deploy a site by choosing a static site generator and a headless CMS and deploy it in minutes with just a few clicks.

JAMStack + headless solves the needs of a majority of the web that is still built on content. And the tooling is nearing a point where there are few, if any, logical reasons not to go with a JAMStack + headless CMS solution for much of the web.