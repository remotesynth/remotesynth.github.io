---
layout: post
title: A Fresh Look at Netlify CMS (Part 2)
date: '2019-05-01'
description: Configuring an existing site to use Netlify CMS
categories:
  - static sites
  - web development
comments: true
---

[Netlify CMS]() is a content management tool designed for [JAMstack](https://jamstack.org/) or static sites created by [Netlify](https://www.netlify.com/) (though it does not require that you use their services). It is designed to work with whatever static site generator you choose - whether it is Jekyll, Hugo, Hexo, or whatever.

In [part one](https://www.netlifycms.org/), I looked at how easy it was to set up a new site using Netlify CMS. In this post, I want to look at adding Netlify CMS to an existing site. In this case, we'll explore adding it to [my personal blog](https://www.remotesynthesis.com/), which uses a pretty standard Jekyll implementation that is already deployed to Netlify.

## Adding the Admin

The first thing I need to do to get this working on my blog, is to add the admin files. The location you'd need to use for this depends on which static site engine you are using and, potentially, your settings. The [documentation](https://www.netlifycms.org/docs/add-to-your-site/#app-file-structure) lists out the standard location that you'd place the admin folder and files for many popular engines. Since I am using Jekyll, the admin folder can go in the project root.

Inside the admin folder, I needed create two files: `config.yml` and `index.html` and place some basic code in there. So as not to completely repeat the documentation completely, the baseline code that needs go in these files can be found [here](https://www.netlifycms.org/docs/add-to-your-site/#app-file-structure).

> Note that you can install Netlify CMS via npm if you prefer. The instructions I follow here would differ, of course.

## Basic Configuration

Pretty much everything you will do for a standard installation of Netlify CMS will be handled in editing the config.yml. There are some advanced features that allow you to create custom widgets and previews in the editor pane that would require additional code, but otherwise it's just about editing the YAML configuration.

Let's take a look at the basic configuration that is already in `config.yml`:

```yaml
backend:
  name: git-gateway
  branch: master
```

The backend here is what will enable my CMS to publish content to the GitHub repository. Since I am hosting this on Netlify, the configuration is simple, but there are [other options and gateways](https://www.netlifycms.org/docs/authentication-backends/) that allow you to use alternatives to GitHub and Netlify if you choose to. The gateway allows these commits to happen without needing to give each user access to the repository itself. Obviously, the branch is the branch where any edits made in the CMS will be committed.

The next thing I need to specify in the basic configuration is where I want to place images and other media that are uploaded. I have a subfolder within my root images folder to place these, so I'll add the following to my YAML `media_folder: "images/posts"` (note that this line should not be indented).

## Configuring Content Collections

Next, I need to configure the CMS so that it knows where my content is. Since this is a fairly standard Jekyll blog, my posts all live in the `_posts` folder and I use fairly standard front matter. Here's an example of the front-matter in a post - this becomes important to configuring the editor.

```yaml
---
layout: post
title: "Promoting Perceived Performance with Prefetching"
date: "2019-04-24"
categories:
    - web development
    - general
description: A look at two libraries designed to help improve the perceived performance of web apps
comments: true
---
```

Those of you that know Jekyll will recognize that this is pretty much the default front matter, so the collection configuration is similar to the example shown in the [documentation](https://www.netlifycms.org/docs/add-to-your-site/#collections). The one significant addition is the use of multiple categories. This makes use of the [list widget](https://www.netlifycms.org/docs/widgets/#list) in the editor that works for handling multiple items like this. Specifying a widget determines how the field is edited in the editor, and there are a number of [default widgets](https://www.netlifycms.org/docs/widgets/#default-widgets) built into Netlify CMS.

Here's what my final posts configuration looks like:

```yaml
collections:
  - name: "blog"
    label: "Blog"
    folder: "_posts"
    create: true
    slug: "{{year}}-{{month}}-{{day}}-{{slug}}"
    fields:
      - {label: "Layout", name: "layout", widget: "hidden", default: "blog"}
      - {label: "Title", name: "title", widget: "string"}
      - {label: "Publish Date", name: "date", widget: "datetime"}
      - {label: "Categories", name: "categories", widget: "list"}
      - {label: "Description", name: "title", widget: "string"}
      - {label: "Body", name: "body", widget: "markdown"}
      - {label: "Comments", name: "comments", widget: "hidden", default: "true"}
```

## Enabling Authentication

Before I can test that my configuration works, I need to enable authentication. Since I am using Netlify to host my site, I'll utilize the [Netlify Identity](https://www.netlify.com/docs/identity/) feature that is already supported in Netlify CMS (again, using Netlify is not required though and other authentication methods are supported).

The first step is to enable identity in the admin.

![enable identity](/images/posts/netlifycms2/identity.png)

Next I need to make identity invite only under settings. The Netlify free account allows for up to 5 invites (obviously, if you need more you can add them and they will be charged based on usage).

![enable invite only](/images/posts/netlifycms2/invite-only.png)

You can optionally allow third-party authentication (example: Google authentication) but, since this is my blog alone, I stuck with basic Netlify authentication.

I also need to enable the git gateway that I mentioned earlier in the configuration (this is also under settings).

![enable git gateway](/images/posts/netlifycms2/git-gateway.png)

Next, I need to add identity script to `index.html` for the admin and on my main home page:

```
<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
```

There is additional script in the [documentation](https://www.netlifycms.org/docs/add-to-your-site/#add-the-netlify-identity-widget) that should also be added to the site's `index.html` page.

Once I reload the admin now in local testing I get this screen to set the site's URL.

![local testing](/images/posts/netlifycms2/local-testing.png)

However, once that is done I still cannot log in because I have not actually invited myself to be an admin in the CMS. I go back in the Netlfiy admin do that (one very minor issue I ran into is that I couldn't accept the invite without pushing the admin live or copying/modifying the URL linked in the confirmation email as the link went to the live URL). I should also note that even local tests will push changes to GitHub and post content live, so be careful (you can enable the [editorial workflow](https://www.netlifycms.org/docs/add-to-your-site/#editorial-workflow) if you want to prevent pages from automatically going live).

To invite myself I go to Identity in the Netlify admin and "Invite Users."

![invite users](/images/posts/netlifycms2/invite-users.png)

To complete the process, I register using the invite.

![register](/images/posts/netlifycms2/complete-signup.png)

Once all of these changes are pushed live, I am already able to add and edit posts!

![editing posts](/images/posts/netlifycms2/posts.png)

## Editing Pages and Data

Beyond just blog posts, I also wanted to edit my "About Me" page via the CMS. Since this is the only real standalone page with content on my site I added it using a [file collections configuration](https://www.netlifycms.org/docs/collection-types/#file-collections). The difference between this and the [folder collections](https://www.netlifycms.org/docs/collection-types/#folder-collections) is that I have to specify each file individually. It's perfect for a one-off page like this or for pages that have differing front-matter configurations.

Here's the configuration I used under `collections` in my config to enable editing of my about page - you'll notice that, in this case, it's not that different from the folder configuration above:

```yaml
- name: "pages"
    label: "Pages"
    files:
      - name: "about"
        label: "About Page"
        file: "_pages/about.md"
        fields:
          - {label: "Layout", name: "layout", widget: "hidden", default: "blog"}
          - {label: "Title", name: "title", widget: "string"}
          - {label: "Permalink", name: "permalink", widget: "string"}
          - {label: "Body", name: "body", widget: "markdown"}
```

Lastly, my list of publications and presentation are generated from [Jekyll data files](https://jekyllrb.com/docs/datafiles/) consisting of YAML data. This kind of editing can be set up using the files configuration as well.

For example, the data about my session recordings was fairly simple YAML.

```yaml
videos:
  -   name: "March 2016"
      title: "Static Sites for JavaScript Developers"
      URL: "https://www.youtube.com/watch?v=TJ3lj-xasdw"
  -   name: "July 2015"
      title: "Not Your Grandad's Static Sites"
      URL: "https://www.youtube.com/watch?v=TJ3lj-xasdw"
 ...
```
 
 And to edit this, I set it up as a list widget with the fields you see above.
 
 ```yaml
- name: "data"
  label: "Data"
  files:
    - name: "videoslist"
      label: "Videos"
      file: "_data/videos.yaml"
      fields:
        - name: "videos"
          label: "Videos"
          widget: list
          fields:
            - {label: "Name", name: "name", widget: "string"}
            - {label: "Title", name: "title", widget: "string"}
            - {label: "URL", name: "URL", widget: "string"}
 ```

You can see what the editor looks like below once the individual field has been expanded.

![editing simple data](/images/posts/netlifycms2/simple-data.png)

The preview pane here doesn't look great but it's ok for my own purposes. If you were building this for a client, however, this may be a place that you rely on creating [custom preview widgets](https://www.netlifycms.org/docs/customization/).

My publications and presentations data lists are a little bit more complex because they have lists within lists.

```yaml
publications:
  - name: "O'Reilly Media"
    articles:
      - title: "Static Site Generators - Modern Tools for Static Website Development"
        URL: "http://www.oreilly.com/web-platform/free/static-site-generators.csp"
      - title: "Working with Static Sites (co-author with Raymond Camden)"
        URL: "http://shop.oreilly.com/product/0636920051879.do"
  - name: "CSS Tricks"
    articles:
      - title: "What Really Makes a Static Site Generator?"
        URL: "https://css-tricks.com/really-makes-static-site-generator/"
...
```

Luckily you can nest list widgets within list widgets.

```yaml
- name: "pubslist"
  label: "Publications"
  file: "_data/publications.yaml"
  fields:
    - name: "publications"
      label: "Publications"
      widget: list
      fields:
        - {label: "Name", name: "name", widget: "string"}
        - name: "articles"
          label: "articles"
          widget: list
          fields:
            - {label: "Title", name: "title", widget: "string"}
            - {label: "URL", name: "URL", widget: "string"}
```

The editor is a bit more complex for obvious reasons.

![editing complex data](/images/posts/netlifycms2/complex-data.png)

> It's worth noting here that during development I often wouldn't see changes like the additional collections listed here in the local admin right away for some reason, even when I'd pushed the changes live as well. This may have just been some sort of caching, but I mention it in case you run into it.

## Finishing Up

I should emphasize that I did not cover anywhere near all the configuration options and features in Netlify CMS. This was all really just the basics. However, all in all, I reiterate the feelings I expressed in the first part of this series - Netlify CMS has really come a _long_ way. For many sites, the editing capabilities it provides are more than sufficient and, as a developer, it was pretty easy to get up and running - both as a new install and adding to an existing site.

Importantly, Netlify is maintaining this as an open source project, meaning that you can [contribute](https://www.netlifycms.org/docs/contributor-guide/) or [fork it](https://github.com/netlify/netlify-cms) (it's under an MIT license). This is already encouraging new tools that utilize the CMS features. In a follow up post to this series, I'll take a look at one of them that has just been released.
