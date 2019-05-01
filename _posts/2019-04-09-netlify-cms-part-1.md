---
layout: post
title: A Fresh Look at Netlify CMS (Part 1)
date: '2019-04-09'
description: Setting up a new site using Netlify CMS
categories:
  - static sites
  - web development
comments: true
---

When I wrote the chapter on "Adding a CMS" for the [O'Reilly static sites book](http://shop.oreilly.com/product/0636920051879.do), which is now two years old, I had the opportunity to check out a brand new project called [Netlify CMS](https://www.netlifycms.org/). It was so new that when I'd reviewed it to write the chapter, it was not even public yet.

So, I was not surprised when I recently had the chance to check out the project that a lot had changed. I was surprised, though, at how dramatic the change was. For example, I'd spent about five pages of the book walking through the configuration that you can now accomplish with a single button click. So, for this post, let's take a look at what Netlify CMS is and how to get started using a template. Future posts in this series will look at setting this up on an existing site and various configuration options for advanced setups.

## What is Netlify CMS

Netlify CMS is a content management tool designed for [JAMstack](https://jamstack.org/) or static sites. It is created by [Netlify](https://www.netlify.com/), but does not require that you use their services in any way. One of the things that has always made Netlify CMS powerful is that it is designed to work with whatever static site generator you choose - whether it is Jekyll, Hugo, Hexo, or whatever.

Once added to your site and properly configured, Netlify CMS offers a simple user interface for adding and editing content that will be much more familiar for users who are comfortable in a Wordpress-like WYSIWYG interface.

For example, below shows the editing and preview for a very simple "about us" page with very limited "front matter" metadata.

![netlify cms admin wysiwyg](/images/posts/netlifycms/netlifycms-admin.png)

## Setting Up Netlify CMS on a New Site

The simplest way to set up a fresh Netlify CMS install is to use one of the predefined templates on [netlifycms.org](https://www.netlifycms.org/docs/start-with-a-template/) and use the deploy on Netlify button. You can choose from Hugo, Gatsby or Middleman as the static site engine of your choice.

The real-time recording below shows how quickly this will set up the basics of a site.

![setting up a new netlify cms site](/images/posts/netlifycms/set-up-new-site.gif)

During the deploy process, the template will automatically send an invite to the owner of the Netlify account.

![invite](/images/posts/netlifycms/invite.png)

Click "Accept the invite" and you'll be sent to the new site and prompted to create a password.

![creating a password](/images/posts/netlifycms/password.png)

Once you do, you are dropped into the admin.

![netlify cms admin main page](/images/posts/netlifycms/admin.png)

All of this works because the template is configured to use the [Netlify identity service](https://www.netlify.com/docs/identity/) to authenticate. If you want to add more users, you would go to your Netlify account admin, click the "Identity" tab at the top and then "Invite users" (the free account allows you to invite up to five users).

![invite new users](/images/posts/netlifycms/invite-new.png)

There are a lot of configuration options for the identity service in Netlify. For example, you can even configure your admin to allow authentication via external providers, like Google authentication. Just go to "Settings > Identity" within your Netlify admin to configure this service (some options do require a paid account).

## Next Steps

Now that we have the site set up, the next steps would look something like:

1. Pull a local copy the GitHub repository.
2. Customize the look and feel of the site.
3. Modify the configuration of Netlify CMS as needed

The last step requires editing of the `config.yml` configuration file for Netlify CMS. This is always within the `admin` folder for the CMS, but the exact location of depends on which engine you are using. In my case, I used Hugo, so it was in `/site/static/admin/`.

![netlify cms configuration file](/images/posts/netlifycms/config.png)

In a future post in this series, we'll go into more detail about the configuration as well as how you can add Netlify CMS to an existing site.
