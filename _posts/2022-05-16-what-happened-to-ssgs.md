---
layout: post
title: When an SSG Isn't Just an SSG, What Is It?
date: "2022-01-18"
description: Many tools we still call SSGs don't produce static-only content.
categories:
  - Jamstack
comments: true
---

Sometimes the technology that a term refers to evolves beyond the literal meaning of the term. This post is about just such a case.

As most of you know, SSG stands for static site generator. It's a term that has been around a long time. Back when I first got into using SSGs around 2013, it referred to tools like Jekyll, Middleman and Hugo, among others. While each had a different approach, they all essentially worked the same.

An SSG would take markup (usually a combination Markdown and HTML), a template (something like Liquid but there are many), data files (YAML, TOML, JSON) and perhaps things like Sass for CSS and CoffeeScript (gasp! but it was 2013) for JavaScript. It would run a build step and produce static HTML, CSS and JavaScript. Here's a diagram I used to use to illustrate what an SSG did.

![old skool SSG](/images/posts/ssg.png)

## The Times They Are A-Changin'

That definition of an SSG stood for many years until about 2019 with the introduction of [Next.js 9](https://nextjs.org/blog/next-9#automatic-static-optimization). Prior to Next 9, Next.js did support static export, but it was an all or nothing affair, meaning that you had to choose to build your site entirely as server-side rendered or entirely as static. This already stretched the definition of a _static_ site generator, but, to be fair, Next.js never called itself that and started its existence as SSR-only.

Next 9 introduced "automatic static optimization" whereby a page could be statically rendered if Next.js determined the page did not have blocking data requirements within `getInitialProps`. Later versions introduced new methods like `getStaticProps` and `getServerSideProps` to allow developers to specify if a page should be server rendered or statically generated.

For quite some time Next.js was alone in this innovation. Many of us lumped Next.js into the SSG category because it shared many capabilities of SSGs and likely also because you could ultimately deloy it to many of the same services that you'd deploy your SSG-based site.

## A Change Would Do You Good

The success of Next.js and the demands of developers spurred other tools within the loose SSG umbrella to adopt a similar "not just static" set of rendering options. Here are a few significant examples:

- Gatsby added server-side rendering as an option starting with Gatsby 4 which was [released last October](https://www.gatsbyjs.com/blog/whats-new-in-gatsby-4/).
- Nuxt added the ability to specify [specific routes to prerender](https://v3.nuxtjs.org/guide/deploy/static-hosting/#advanced) in Nuxt 3 which went beta in October 2021 and released a [release candidate in April](https://nuxtjs.org/announcements/nuxt3-rc).
- Astro, a new tool that began as exclusively static rendering, added support for SSR [in April](https://astro.build/blog/experimental-server-side-rendering/).
- Eleventy added the [serverless plugin](https://www.11ty.dev/docs/plugins/serverless/) as of version 1.0, which had it's [stable release in January](https://www.11ty.dev/blog/eleventy-one-point-oh/).

As you can see, the ground shifted quite a bit in the past year alone. It was one thing to lump a tool like Next.js into the SSG umbrella as an outlier (yes, Nuxt did previously support an all-or-nothing SSR/static generation option too), but now tools that were traditionally pure SSGs like Gatsby and Eleventy suddenly allowed non-static routes.

## Don't You Forget About Me

There still exists a still popular set of tools that stay true to the SSG definition like Hugo and Jekyll, but it's clear that most of the tools are moving on from purely static output.

Is it fair to lump a tool that supports SSR and even perhaps [other types of rendering](https://bejamas.io/blog/understanding-rendering-in-the-jamstack/) in with tools that export purely static output under the umbrella of static site generators? Probably not.

Has anyone come up with a better term? I don't think so. At least, not yet anyway.

So we keep using the SSG name even if it's a misnomer. At some point, though, we'll have to reckon with a very ill-fitting name for these tools, because naming is important in the end. A misleadingly named set of tools can lead to confusion which hurts adoption, muddles the message and leaves an opening for folks who, for whatever reason, don't like these particular tools.

So what's a better name? It's not easy since these aren't exactly frameworks though they may be based on frameworks (Next.js is often referred to as a metaframework) but tools like Eleventy and Astro aren't based on frameworks either. Maybe dynamic site generator. Or dynamic web application generator. Or dynamic web application builder. Maybe just web application builder.

Ideas? Share them with me [on Twitter](https://twitter.com/remotesynth).
