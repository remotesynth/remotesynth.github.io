---
layout: post
title: "5 Common Problems with Technical Articles"
date: "2016-02-11"
categories:
    - content strategy
description: Common mistakes most developers tend to make in their writing.
comments: true
---

I read and edit a lot of technical articles - generally written by developers for developers. In the past, I wrote up some guidelines for [making your technical content better](http://remotesynthesis.com/general/2015/05/18/writing-for-tech-audience/). This time, I want to take the opposite angle and focus on some mistakes I see all too frequently.<!--more-->

## The Intent Isn't Clear

The background to whatever you are covering can be important. But make sure the intent of your article is clear _before_ diving into a long background explanation. In fact, I'd say you should have a clear, one-sentence (preferably) explanation of what the article intends to explain/show within the first paragraph of your intro. The background can come after this.

Make the intent crystal clear too. A typical feature tutorial might have something like:

> In this article I intend to demonstrate what the new arrow functions in ES6 are, why they are useful and how to incorporate them into your application.

Or an opinion article might say:

> I'm going to discuss why I believe ES6 arrow functions are a useless feature that you'll probably never use, but first, let's discuss what they are.

\* To be clear, I'm making these up as examples.

**Why?** Because most readers won't get through paragraphs worth of background before clearly understanding what you intend to discuss. You may feel that the background leads into the intent and doing it this way comes out "backwards," but your reader just wants to know what they will get out of it before committing their time to the rest (and titles are generally too short to make the scope of the article perfectly clear).

## The Context is Too Narrow

Oftentimes, the actual code we're sharing shows how to do something very narrow. This is usually because we are sharing code from a problem we were solving in a specific application for a speific purpose. However, the concepts we cover can be much more broadly applicable.

For example, perhaps you are writing an article that walks through the code of a Jekyll plugin you created to generate multiple output pages for a single post Markdown (again, making this up). Rather than fixating on the specifics around what the plugin does, you should show how it illustrates building a Jekyll plugin and how you learned about and used some of the internals of Jekyll to figure out how to build it.

**Why?** Because the specifics of your code may only really be applicable to a handful of people (if anyone, depending on the nature of what you are working on) but the concepts are likely useful to a much broader audience. If you are taking the time to write this up, I assume you want people to actually read it.

## Unexplained Code

Developers tend to believe that code is, for the most part, self explanatory. I've seen many articles take a sample and simply paste large chunks of code with little to no explanation. The truth is, even with some inline comments in the code, this not only makes for a rather uninteresting read, but can confuse many readers.

For example, let's imagine I am using the following code sample:

{% highlight liquid %}
{%raw%}
<!-- offset 2 -->
{{ range $index, $element := .Site.Pages }}
    {{ if gt $index 1 }}
    <li>
        <span class="date">{{ .Date.Format "Jan" }}
        <strong>{{ .Date.Format "2"}}</strong></span>
        <h3><a href="link">{{ .Title }}</a></h3>
        <p>{{.Description}}</p>
    </li>
    {{ end }}
{{ end }}
{%endraw%}
{% endhighlight %}

I might say:

> In the above example, we are looping through a list of posts in Hugo, starting with the 3rd most recent post. We do this within our `range` loop by checking the index (which, in Go, starts at 0). Within this loop, we output the month and day of the post, each formatted for the constraints of our layout, as well as the full title and description.

Of course, this is a very simple and slightly contrived example, but hopefully you get the idea. Some people prefer to go line by line, which, in code that isn't as markup focused as this one, can work well as well. The point is, don't treat your readers like idiots, but don't assume they know what's going on just by looking at your code.

**Why?** I'd argue there are three good reasons to fully explain your code samples. The first is that you cannot know the experience level of all of your readers, and what seems obvious to you, may not be obvious to them. Second, unexplained code often leads to improperly copied code - the reader thinks the code solves their issue but doesn't understand everything it is doing (which, you'll probably end up explaining via a response to a frustrated comment anyway). Third, it makes the article more interesting as it often leads to discussion of why you chose a particular solution or how some feature of what you are writing about works internally.

## Lack of a Consistent Voice

This is less of a major issue then a nitpicky one on my part perhaps (and one I am occassionally guilty of myself), but when writing a tutorial, choose I, we or you and stick to it. So many articles move from "next we'll do this" to "once you edit this line" to "I chose to use x." Oftentimes, this is compounded by switching between present and past tense. It's distracting as a reader.

Personally, I prefer to use "we" because I find it friendlier (you sounds too commanding and I can make it sound like too impersonal). Of course, opinion articles will be a lot of I (in fact, as a sidenote, if you are writing an opinion, you should not intentionally or unintentionally assume you are speaking for your audience by using we). I also prefer present tense because it gives a sense that we are actively working together in the moment.

For example:

> In the above code, I'm looping through a list of posts in Hugo, starting with the 3rd most recent post. You can do this within our `range` loop by checking the index. Within this loop, we will output the month and day of the post. We also displayed the title and the description.

Should be:

> In the above code, we're looping through a list of posts in Hugo, starting with the 3rd most recent post. We're doing this within our `range` loop by checking the index. Within this loop, we're outputting the month and day of the post. We are also displaying the title and the description.

Again, the example is intentionally simple and contrived but hopefully it illustrates the point.

**Why?** The lack of a consistent voice or tense can be distracting and even potentially confusing for your reader - they may even find themselves reading and rereading a line without even realizing why it is confusing. Plus, it simply makes your content lack a level of polish that can be the difference between an ok article and a great article that I want to share.


## No Conclusion

In conclusion, always include a conclusion. Even if your conclusion is short summary of the article restating the key points - add it. It should, preferably, offer other resources to continue learning or some sort of call to action, even if it's just to share their thoughts in the comments.

For example:

> Hopefully this article helps you avoid some common pitfalls that have been holding your content back. While there are no hard and fast rules for what makes a good technical article (and you should always feel free to express your own style), the issues discussed here are ones that I've found can detract from otherwise excellent technical details. Let me know if you agree or disagree with any of my suggestions - or have some additional ones of your own - cia the comments or on [Twitter](https://twitter.com/remotesynth).