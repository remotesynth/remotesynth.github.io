---
layout: post
title: "Developers Need to Start Paying Attention to Licenses"
date: "2017-09-05"
categories:
    - general
description: Ignoring licenses can be dangerous. Let's try to understand them.
comments: true
---

Anyone who claims to be a fan of mashups (which, admittedly, had their moment that seems to have passed) knows [Girl Talk](http://illegal-art.net/girltalk/). Girl Talk (aka Gregg Michael Gillis) had a crazy style of mashup made up of short, somewhat chaotic samples, usually blended together into one full "album"-worth of music.

He was also fearless, sampling from artists that others dared not - both recent hits and classic artists. Looking at the [samples in his "Feed the Animals"](http://www.illegal-tracklist.net/Tracklists/FeedTheAnimals) album from 2008, you'll see literally hundreds of samples making up the 14 tracks.

>  Girl Talk (real name Gregg Gillis) has also won critical praise but is not likely to land a big-time contract, commercial radio play, a spot in an iPod ad or even distribution on iTunes. This is because “Feed the Animals” is composed almost entirely of more than 200 samples of other artists’ music, ranging from Lil Wayne to Kenny Loggins — none of which Gillis has obtained permission to use.
> 
> Rob Walker, [Mash Up Model](http://www.nytimes.com/2008/07/20/magazine/20wwln-consumed-t.html), New York Magazine

Thankfully Girl Talk survived without a lawsuit by citing the [fair use](https://en.wikipedia.org/wiki/Fair_use) doctrine, probably aided by the fact that he frequently just gave away the music for free.

So what does Girl Talk have to do with coding?

## Applications Today are Code Mashups

Today's applications are arguably the equivalent of a Girl Talk album in code. They are made up of code that comes from a variety of sources. For instance, they may use one or more frameworks and libraries each of which may also may rely on hundreds of modules (ex. npm, Ruby gems). Even portions the "original" code in a project may have originally been copy/pasted from documentation, a tutorial or \*gasp\* StackOverflow.

If Girl Talk's music mashups were "[a lawsuit waiting to happen](http://www.nytimes.com/2008/07/20/magazine/20wwln-consumed-t.html)", why aren't our applications?

## Licenses

Pretty much every bit of code we use (even the copy/pasted code) is covered by some form of license (in effect, even code with [no license](https://choosealicense.com/no-license/)). The license determines what you, the developer, can legally do with the code. Can we sell our software that uses the code? Can we redistribute it? Can we use a different license on our code than the code we included? Check the license.

The thing is developers (myself included) rarely ever look at the license. I'm fairly sure the current process is:

1. Google the problem I am trying to solve
1. Find a Github project, blog post, etc. that solves this
1. `npm install` or `gem install` or fork or copy/paste this code into my project.

Rarely do those steps include looking at the license. This gets complicated further by the fact that many of these projects have dependencies that each have their own licenses - all of which my project now needs to abide by. Even if I actually read the license, I'd have to trust that the developer of this project was careful about the licenses of their dependencies. (And what if those dependencies have dependencies?)

Assuming I were to read any or all of these licenses. I am not a lawyer. I may have no real clue what any of them mean.

> I should repeat - _I am not a lawyer_. This post will talk a lot about licenses but it is aimed at giving a rough overview of their meaning. To assess the specific requirements and risks for you or your company, you should probably seek proper legal counsel.

Not paying attention to licensing could open you and your company up to lawsuits and other legal consequences. In order to help you avoid those situations, this article aims to give you an overview of the various types of licenses typically associated with the software and code you may use in a given project. Hopefully this can help you stay aware and navigate the complexities.

## Open Source vs. Closed Source

When we talk licenses, most developers immediately assume "open source." However, there are lots of companies that sell code libraries (including my current employer among many others).

The first mistake I've seen many developers make is to use a commercially licensed library as if it was free and open source. Just because a piece of code is publicly available, whether on a CDN, npm or elsewhere, doesn't mean that you are free to use it.

Here's an example. You can include the entire Kendo UI library (not just the open-source portion of Kendo UI core) via a [CDN](http://kendo.cdn.telerik.com/2017.2.621/js/kendo.all.min.js) and your project will work just fine. However, taking a look at the contents, you'll see this:

```javascript
/** 
 * Kendo UI v2017.2.621 (http://www.telerik.com/kendo-ui)                                                                                                                                               
 * Copyright 2017 Telerik AD. All rights reserved.                                                                                                                                                      
 *                                                                                                                                                                                                      
 * Kendo UI commercial licenses may be obtained at                                                                                                                                                      
 * http://www.telerik.com/purchase/license-agreement/kendo-ui-complete                                                                                                                                  
 * If you do not own a commercial license, this file shall be governed by the trial license terms.       
```
As this makes clear, this is a commercially licensed piece of code. The actual license can be found [here](http://www.telerik.com/purchase/license-agreement/kendo-ui-complete). Because you would be using this software without a purchased license, you fall into the trial license which is defined as:

> 1.1.1 License Grant. If You download the free Trial License, then, subject to the terms and conditions set forth in this agreement, Licensor hereby grants to Licensee and Licensee hereby accepts a license to use the Software for the sole purpose of evaluating its functionality and performance. You are not allowed to integrate the Software into end products or use it for any commercial, productive or training purpose. You may not redistribute the Software. The term of the Trial License shall be 30 days. If You wish to continue using the Software beyond expiration of the Trial License, You must purchase the applicable commercial license.

The important things to note are that you cannot use this "into end products or use it for any commercial, productive or training purpose" - basically, nothing that goes into production. Also, the "term of the Trial License shall be 30 days" - after your 30 days are up, if you don't purchase a license, you are in violation. Note that it doesn't say that you are free to keep using it in non-production apps - the only two options of the license after 30 days are purchase or don't use the product.

The point here is not to single out Kendo UI in any way - there are lots of vendors selling software via similar means with similar licenses (though I don't believe that there is any specific requirements that a commercial license must abide by) - but just to reiterate that just because the code is available does not mean that you can use it.

### What Types of Licenses Qualify as Open Source?

The Open Source Initiative (OSI) is the "stewards of the Open Source Definition (OSD) and the community-recognized body for reviewing and approving licenses as OSD-conformant" according to their [open source definition](https://opensource.org/osd). They have a review process for approving new licenses and maintain a [list of their approved licenses](https://opensource.org/licenses/category) that qualify as open source.

However, it's worth noting that just because OSI has approved a license doesn't mean that the community as a whole agrees that this qualifies as open source. As an example, there has been a lot of talk over the React license recently. React uses a BSD+Patent license (you can see their explanation of the license [here](https://heathermeeker.com/2017/08/19/open-source-community-over-reacts-to-x-rated-code/) and [here](https://code.facebook.com/posts/112130496157735/explaining-react-s-license/)).

Now, technically the [BSD+Patent](https://opensource.org/licenses/BSDplusPatent) is on the OSI compliant list (I am not qualified to speak to whether React's license is implemented fully in accordance with the OSI approved BSD+Patent license). But, the Apache Software Foundation added it to their [category X](https://www.apache.org/legal/resolved.html#category-x) list, which is a list of licenses that cannot be used in an Apache products.

So is the BSD+Patent license used by React open source? In the eyes of the OSI, it would appear so. However, in the eyes of the Apache Software Foundation and many others who blogged on the topic, perhaps not (or at least not in the true "spirit" of open source).

So, to answer the question asked in the heading of this section (what types of licenses qualify as open source?) - it depends. Seems appropriate when we are talking about software I suppose.

## Types of Open Source Licenses

A key item to recognize is that not all open-source licenses are the same. Some allow you a lot of freedom to do what you want (in fact, for some time I used the [WTFPL](http://www.wtfpl.net/txt/copying/) on my code, which is about as permissive as you can get). Other licenses have restrictions in terms of things like attribution, redistribution or the kind of license you can have on any work using the software.

### Permissive Licenses

I think part of the carelessness of developers like me regarding licenses has been because we took for granted the proliferation of extremely permissive licenses like the [MIT license](https://opensource.org/licenses/MIT).

Aside from the WTFPL, which is not an OSI approved license, MIT is probably the most permissive license out there and also one of the shortest in length. Summed up (again, not a lawyer), it gives you permission to basically do anything - "use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so..." The only conditions are that you include a copy of license and agree not to hold the software creators liable for anything.

*(Note: [Wikipedia](https://en.wikipedia.org/wiki/MIT_License#Variants) indicates that there are some variants of the MIT license but the differences are fairly minor.)*

Part of the reason for the MIT license's popularity is probably its simplicity. Even the resources like the [Open Source Guide](https://opensource.guide/legal/#which-open-source-license-is-appropriate-for-my-project) created by GitHub lead developers gently towards the license.

> If you’re starting from a blank slate, it’s hard to go wrong with the MIT License. It’s short, very easy to understand, and allows anyone to do anything so long as they keep a copy of the license, including your copyright notice. You’ll be able to release the project under a different license if you ever need to.
> 
> [The Open Source Guide](https://opensource.guide/legal/#which-open-source-license-is-appropriate-for-my-project)

There are a number of other permissive licenses however. Another very popular option is the [Apache License, Version 2.0](https://opensource.org/licenses/Apache-2.0). Besides being quite a bit lengthier, the difference in the Apache license, according to [Choose a License](https://choosealicense.com/) (also created by GitHub) is the following:

> The Apache License 2.0 is a permissive license similar to the MIT License, but also provides an express grant of patent rights from contributors to users.

This grant of patent rights apparently makes the license more appealing to businesses considering using the software. However, from a developer standpoint there are very few restrictions other than retaining the license, patents and attribution as well as document any changes to the software, but you are still free to do things like redistribute, modify, etc.

The [BSD license](https://opensource.org/licenses/BSD-2-Clause) is another option. It's similar in its requirements to the MIT and Apache licenses (i.e. the software is available "as is" and the copyright notice must remain). 

*(Note: There is a [3-clause](https://opensource.org/licenses/BSD-3-Clause) version that is similar to the MIT variant mentioned above in its protection of the names of the copyright holders.)*

### Copyleft

The key distinction about copyleft open source licenses from permissive licenses is that they limit how you can redistribute or modify the software. Essentially, any work that redistributes or modifies software licensed under a copyleft license must itself be open-sourced using a copyleft license, which is why you'll sometimes hear them referred to as viral licenses (that's my _non-lawyer_ explanation anyway).

The most common copyleft license is the GNU General Public License or more commonly [GPL](https://opensource.org/licenses/GPL-3.0), which is most currently at version 3. Using the GPL v3 license, you _can_ redistribute the code but it must remain open source under the same license in most cases. Essentially, no company can come in and use the code in any closed-source, proprietary applications or even open source, but incompatible licenses. For example, GPLv3 licnesed software cannot be used in an Apache project:

> We avoid GPLv3 software because merely linking to it is considered by the GPLv3 authors to create a derivative work.
> 
> [GPL Compatibility](https://www.apache.org/licenses/GPL-compatibility.html), Apache Software Foundation

The [GNU Lesser General Public License version 3](https://opensource.org/licenses/LGPL-3.0) or LGPL is a slightly less strict version of the GPL (as the lesser in the name implies). The key difference here is that, if I am a company creating proprietary software, I can rely on an LGPL licensed project as a shared library without needing to open source my software's code.

Oftentimes GPL or LGPL licenses will be found in commercial open source projects where the projects may be dual or multi licensed. The free version may be under a GPL license, limiting its use in proprietary software unless the creator wants to commit to also licensing this work as GPL and making the source publicly available. However, under the dual license, the company can purchase a commercial licensed version of the software that does not have this limitation. A common example of this is the many different editions of MySQL, of which the "Community Edition" is the GPL licensed version.

## Other Licenses

Of course, there are a lot of other licenses, both open source and not, available than the ones covered here. If you're an individual or company looking to license your software, you don't even need to use one of the preset licenses - you are free to create your own if you like. That arguably might not be the best use of your resources however.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">File “rolling your own open source license” in the same folder as “rolling your own crypto.” Bad ideas.</p>&mdash; Nicholas C. Zakas (@slicknet) <a href="https://twitter.com/slicknet/status/900446297710186498">August 23, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Of course, if you have the right legal resources, this may not be an issue for you. There are also sites like the [http://www.binpress.com/license/generator](http://www.binpress.com/license/generator) that offer to generate a license for you based upon a number of configurable options.

## Copy/Pasted Code

Before ending this article, I'd be remiss if I didn't cover code copy/pasted from online sources. It's a tough area to cover in great detail not just because their is an endless list of potential sources, but also because the nature of the code you copy may be fuzzy (if you copy one line of commonly used code versus copying the source an entire JS library, for example).

In these cases, it's important to remember that [no license](https://choosealicense.com/no-license/) does not mean that it is public domain.

Let's just look at some common cases.

### StackOverflow

Even those of you who won't admit it have probably copy/pasted code from StackOverflow (aka StackExchange). To the best of my ability to discern, code and content from StackExchange fall under its [terms of service](https://stackexchange.com/legal/terms-of-service) which states that any user created content is licensed under the [Creative Commons Attribution Share Alike](https://stackexchange.com/legal/terms-of-service) (this is also restated in their global page footer).

While this license does [require attribution](https://stackoverflow.blog/2009/06/25/attribution-required/), it is typically used for creative content. Essentially, StackExchange does not want other sites reusing content from their site without attribution.

I did find a post by StackExchange explaining that the [code on their site was MIT licensed](https://meta.stackexchange.com/questions/272956/a-new-code-license-the-mit-this-time-with-attribution-required?cb=1) - however, importantly:

> Attribution now continues to be required when you use code found at Stack Overflow and Stack Exchange.

That being said, when searching for code on the site, I find no mention on the page of this licensing, which is supposed to have been in effect since March of last year. Attribution of a chunk of code easily attributable to StackOverflow can be just a comment with the URL where the code was originally found.

### Books

The license of code provided in books (whether digital or hard copy) seems to vary based on the publisher. O'Reilly stood out when I investigated this as they directly state that any code provided is available for use without permission or even attribution (though it does, of course, say attribution is appreciated).

In reviewing other books in my possession, however, most did not specifically state the license of the code contained within. Others contained some form of liability waiver for the code and content, but no direct license or terms (one such publisher's license could, in my non-lawyerly opinion, be read as both a very restrictive license that applied to the code as well as a liability waiver). In some other cases, where the code is separately downloadable, you should follow any license included within that code (if one is provided).

### Blogs and Documentation

In searching for examples, I found that it is very hit or miss whether any blogs or documentation is ever explicitly licensed - even in the case of documentation for commercial libraries.

In the case of documentation, one would argue that this code is being shared _with the intent to be reused_, but it's worth checking the license of any code where you are copying a significant portion that is attributable to a specific documentation source. If no license is provided and you have concern, then contact the owner or company for more details.

When it comes to blogs, oftentimes the license for the code is contained in relevant linked repository or code snippet sharing tool (for example, public CodePen's are [automatically MIT licensed](https://blog.codepen.io/legal/licensing/)) being used. Otherwise be cautious when copying significant portions of code from a site that does not provide a license for the content and code.

## Learning More

Hopefully this article gave you enough of an overview of licenses that you have a basic understanding of what you are getting into when including a third-party resource into your next development project. The goal here is not to become paralyzed with concern about licenses, but just to make sure that you have a solid sense of what you're getting into and, for sure, don't ignore the license before moving forward.

There are a ton of useful resources available if you want to delve further, some of which I relied heavily upon for this article.

* GitHub's [Choose a License](https://choosealicense.com/) site is great for both project creators or anyone looking for a relatively clear explanation of existing licenses and their restrictions or requirements. A similar but brief summary is provided by GitHub as well in their [Open Source Guide](https://opensource.guide/legal/#which-open-source-license-is-appropriate-for-my-project)
* Smashing Magazine published [A Short Guide To Open Source Licenses](https://www.smashingmagazine.com/2010/03/a-short-guide-to-open-source-and-similar-licenses/) by Cameron Chapman that covers a short list of open source licenses (including the Creative Commons, which I didn't cover here since it typically is not used for code).
* Wikipedia offers a [table comparing open source licenses](https://en.wikipedia.org/wiki/Comparison_of_free_and_open-source_software_licenses) that can give you a quick glance over a long list of licenses and requirements.
* The [tldrlegal](https://eladnava.com/check-your-dependencies-license-requirements-with-tldrlegal/) library aims to give you a quick overview of any licenses within your project's npm dependencies relying on [tldrlegal.com](https://tldrlegal.com/) for simple license explanations.

*Thanks to [TJ VanToll](https://twitter.com/tjvantoll) and [Jeremy Meiss](https://twitter.com/jerdogxda) for reviewing this article for me*