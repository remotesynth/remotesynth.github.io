---
layout: post
title: Building and Deploying a JAMStack site with Stackbit
date: '2019-05-06'
description: A quick introduction to using the Stackbit service for creating a content-managed JAMStack site
categories:
  - static sites
  - web development
comments: true
---

In recent weeks, I've discussed how to [start a new site from scratch with Netlify CMS](https://dev.to/remotesynth/a-fresh-look-at-netlify-cms-part-1-136k) and how to [modify an existing site to use Netlify CMS](https://dev.to/remotesynth/a-fresh-look-at-netlify-cms-part-2-5694). However, the tooling around JAMStack also continues to improve to where there are tools that are being created to further simplify the process of developing a content managed JAMStack site.

In this post I want to take a look at one of those tools that is currently in an early beta release called [Stackbit](https://www.stackbit.com/). As we'll see, the benefit of Stackbit is that you can choose a template and deploy a JAMStack site with CMS integration and deploy this to Netlify, all without touching a single configuration file or writing a single line of code.

> Note that I was given access to Stackbit as a beta user, but I am not in any way affiliated with the company nor have I been asked for an endorsement of any sort.


## Getting Started with Stackbit

To start off, you'll need to request a [beta invite](https://www.stackbit.com/beta/) to Stackbit. Once you have that, here's how you get started.

Once you have an account and log in, you'll want to create a new project.

![create a new project](/images/posts/stackbit/new-project.png)

You'll want to give it a name or stick with a default and then select a theme. There are a handful of nice, simple themes available in the beta and they each include a live preview. Using a custom theme is an option, but, at the moment, you'll need an additional beta invite to use this feature (however, since this is all deployed to GitHub, you can do whatever with the deployed code after the project is created, including customizing the theme). It's also important to note that you cannot change themes once your project is created.

![choosing a theme](/images/posts/stackbit/choose-theme.png)

Next, you choose which generator you would like to use to build the site. Currently Stackbit supports three of the most popular engines: [Jekyll](https://jekyllrb.com/), [Gatsby](https://www.gatsbyjs.org/) and [Hugo](https://gohugo.io/). Vuepress and Hexo support is coming soon.

![choose an engine](/images/posts/stackbit/choose-generator.png)

The final choice is a your backend CMS. Once again, Stackbit offers support for the most popular options such as [Forestry](https://forestry.io/), [Netlify CMS](https://www.netlifycms.org/) and [Contentful](https://www.contentful.com/). Forestry and Contentful are commercial options that may incur additional costs depending on your requirements. Netlify CMS is free but may not be as full featured as you require depending on your site (for example, Contentful has an API that would allow you to reuse the content on a mobile app). [Prismic](https://prismic.io/) support is coming soon. You can also choose to have no backend if you prefer.

![choose a backend](/images/posts/stackbit/choose-backend.png)

Once you've made all the choices, all you need to do is connect the relevant accounts. You'll need to connect Github and Netlify at a minimum, although, if using one of the other CMS services, you'll need to connect those as well.

![connecting accounts](/images/posts/stackbit/connect-accounts.png)

The site is automatically created, pushed to GitHub, connected to and deployed to Netlify. If you're using Netlify CMS, it will automatically invite you to be an editor.

![going live](/images/posts/stackbit/deploying.png)

## Next Steps

Congrats, you deployed a fully content-managed JAMStack site!

![deployed](/images/posts/stackbit/deployed.png)

At this point, from the Stackbit admin, you can go to the CMS admin or the site, but not much else (other than delete the site on Stackbit, which, I should note, doesn't delete the site on Github or Netlify). However, as I mentioned before, you are free to pull the code from GitHub and customize to your heart's content.

It's still early for Stackbit but it definitely shows some promise as an option for quickly getting a content-managed JAMStack site up and running. I'm looking forward to seeing how they continue to evolve the tool.