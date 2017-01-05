---
layout: post
title: "More Advanced Jekyll/Liquid Template Techniques"
date: "2016-10-27"
categories: 
    - web development
    - static sites
description: Sometimes Jekyll stuff isn't obvious.
comments: true
---

Working on a recent project, I've come across several items that were either not well documented or slightly complex - though perhaps calling them "advanced" overstates the case. In this case, we'll cover using multiple filters on a single value, using Liquid in Markdown, custom sorting posts and displaying posts by category. I'm sure there may be different (even better) solutions to what I describe here, but I share because these worked for me (and might for you too).

> In case you missed it, I published my original [Advanced Jekyll/Liquid Template Techniques](http://www.remotesynthesis.com/general/2015/10/02/advanced-jekyll-templates/) about a year ago that covers determining if a category has posts (and how many), assigning variables, using variables in an include and, finally, dynamically loading data based on a variable.<!--more-->

## Use Multiple Filters on a value

This one is kind of trivial and may be obvious to most people, but I didn't see it clearly documented (and most examples show using a single filter). All you need to do is add another pipe and another filter.

{% highlight liquid %}
{%raw%}{{ mystring | replace: "-", " " | capitalize  }}{%endraw%}
{% endhighlight %}

## Use Liquid in Your Markdown Posts

This one may also be in the category of "duh!" but you can use Liquid code in your Markdown. So, in this case, I needed the relative path to an image to work on the remote site and on the local testing server.

{% highlight liquid %}
{%raw%}![My awesome image]({{ "/img/my-awesome-image.png" | prepend: site.baseurl }}){%endraw%}
{% endhighlight %}

## Sorting Posts by Something Other Than Date

By default, Jekyll posts come in descending date order. However, I was building a documentation site and using posts as a way to add content to a single page with content separated by anchors (basically, a variation of the [documentation site that I built with Hugo](https://github.com/cfjedimaster/Static-Sites-Book/tree/master/ch4/docsite) for the [upcoming book](http://shop.oreilly.com/product/0636920051879.do) I'm writing with Raymond Camden). In this case, I wanted to be able to specify what order the content would display without needing to fiddle with the post dates.

[Hugo](https://gohugo.io/) has the concept of [weight](https://gohugo.io/templates/variables/), which is helpful - especially since the weight is relative to other items in the category. While nothing like that exists in Jekyll, we can add it and even sort by it (though not in exactly the same manner as Hugo). Assuming that each of your posts has a `weight` value set in its frontmatter, you can do the following:

{% highlight liquid %}
{%raw%}{% assign posts_list = site.posts | sort:"weight" %}
{% for posts in posts_list %}
{% endfor %}{%endraw%}
{% endhighlight %}

You don't have to sort by weight. You can sort by any frontmatter value - weight just suited my needs in this scenario.

## Displaying Posts Organized by Category

Following on the sorting technique above, for this docs site, the left nav is essentially a category name and then a list of the posts within that category. In the below code, I loop through the posts (sorted by weight) and display the category header assuming the post's category is different from the prior post (of course, this assumes that the content is organized properly by weight).

One other thing you may notice is that I ignore posts with no title. In the case of my single page documentation site, some sections had "intro" text that would display in the content but doesn't require a navigation link. Thus, if I left the title blank, I will display it in the main content output but not in the navigation. You can also see that I am using the `post.slug` variable as a way to anchor the links rather than directly link to the page.

{% highlight liquid %}
{%raw%}<ul class="docs-nav">
{% assign posts_list = site.posts | sort:"weight" %}
{% assign last_cat = "" %}
{% for posts in posts_list %}
    {% if posts.title != "" %}
        {% for category in posts.categories limit:1 %}
            {% if category != last_cat %}
    <li><strong>{{ category | replace: "-", " " | capitalize  }}</strong></li>
            {% endif %}
            {% assign last_cat = category %}
        {% endfor %}
    <li><a href="#{{ posts.slug }}" class="cc-active">{{ posts.title }}</a></li>
    {% endif %}
{% endfor %}
</ul>{%endraw%}
{% endhighlight %}

## That's All For Today!

I know that none of this may be earth-shattering, but they are all things that I found not obvious (and I've clearly used Jekyll a good amount). If you are curious, this code was for the documentation for an [Angular Multi-Platform Starter](https://jlooper.github.io/angular-starter/) project that I am working on with some of my colleagues.