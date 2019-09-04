---
layout: post
title: Understanding OAuth Authorization Flows
date: '2019-09-04'
description: What happens when you authenticate in an application using OAuth 2.0 implicit and PKCE flows.
categories:
  - web development
comments: true
---

If you've used things like Google Sign In, Twitter authentication or GitHub authentication (to name a few common examples), or enabled integrations in other web applications, then you are probably familiar with OAuth.

However, even if you've had to fully implement this yourself, if you're like me, you may not have thought too deeply about what is going on behind the scenes - during the OAuth authentication flow. In this post, I'm going to share a high level explanation of the standard OAuth 2.0 flow - called the implicit flow - for web applications. We'll then dig into the PKCE extension (don't worry if you don't know what that is yet) and explain why best practice recommendations today suggest using that flow.

_I should quickly note that I am not an expert on OAuth but have spent some time digging into this topic lately and thought it would be useful to share what I've learned. Please comment on any suggestions for how I can improve the information in this post._

## The Implicit Flow

From a user standpoint, the authentication flow is pretty simple. Let's say I click a button that says "Sign in with GitHub." I am then sent to GitHub to sign in and, if this is my first time, grant permissions. Once this is done I am sent back to the original site and - voilà! - I'm logged in.

As you'd imagine, behind the scenes there's a bit more going on. The basic steps are as follows (yes, this is a simplified version):

![the OAuth 2.0 implicit flow](/images/posts/oauth/sm_implicit_flow.png)<br>
_The implicit flow expressed entirely in emoji_

1. The application requests authorization from the user
1. The user authorizes the request
1. The authorization server issues an access token via the redirect URI
1. The application uses the token to call the API

The steps in the implicit flow are pretty straightforward and, if you've implemented OAuth 2.0 in a web application, this is probably the flow you are familiar with. A key aspect to notice is that token necessary to access the API is passed via the redirect.

## Security Considerations Around the Implicit Flow

Security on the web is always about trade-offs - more security usually means more complexity. Despite how it may seem above, the implicit flow is actually extremely simple. While this has worked and continues to work for a wide range of web applications, security experts had (and continue to have) concerns that it leaves open some potential attack vectors.

The primary vulnerability revolves around the fact that a valid access token is returned via the redirect. As [Brock Allen states](https://brockallen.com/2019/01/03/the-state-of-the-implicit-flow-in-oauth2/):

> The aspect of the implicit flow that is most criticized as difficult to protect is also the fundamental mechanic of what defines the implicit flow, namely that the access token is returned from the token server to the client from the authorize endpoint.

Some of the concerns include:

* A "man in the middle" attack can intercept the redirect, thereby gaining a valid access token.
* An access token can be injected into the redirect URL and there is no validation mechanism to ensure that the token wasn't maliciously injected.
* The redirect in-and-of-itself can be stored in browser history (and even replicate to the cloud) thereby ensuring that copies of a valid access token have the potential to leak.

That is not to say that the implicit flow is insecure - and there are practices for mitigating these issues. However, some of of these issues were considered acceptable trade-offs in 2012 when the spec was created, largely because browser limitations in cross-domain access back then limited the availability of more secure options.

> A good overview of the potential threats in the implicit flow and the available mitigation strategies are discussed in [OAuth 2.0 for Browser-Based Apps](https://tools.ietf.org/html/draft-parecki-oauth-browser-based-apps-02#section-9.8).

## What is PKCE?

PKCE (which stands for "Proof Key for Code Exchange" and is pronounced "pixie") was originally developed to solve a problem specific to native mobile apps using OAuth 2.0. The problem was that the application secret could not safely reside in the app. On a web app, this would sit on the server, never accessible to the client before it is passed to the authorization server. However, a mobile app would need to have it reside within the application code, which could be revealed during a decompiling process. In addition, custom URL schemes used in mobile apps for the redirect could potentially be compromised.

PKCE was an extension to OAuth 2.0 that resolved this problem by adding some steps to the process.

![the OAuth 2.0 PKCE flow](/images/posts/oauth/sm_pkce_flow.png)<br>
_The PKCE flow expressed entirely in emoji_

1. The application requests authorization from the user and "code challenge" is created using a random "code verifier"
1. The code challenge is sent to the authorization server and the user authenticates
1. The authorization server stores the code challenge and returns a code to the application
1. Application sends the code and code verifier to authorization server via a POST request
1. The authorization server verifies the code challenge/code verifier and issues an access token via a POST response
1. The application uses the token to call the API

While the PKCE flow is clearly more complicated, there are some key differences to notice. First, there is no preconfigured secret. Instead PKCE uses a cryptographically random code verifier that is generated for each request. There is also no redirect to intercept. A "man in the middle" attack could only steal the authorization code but won't have access to a valid token, and because there is no redirect, there is also no browser history potentially containing a valid token.


## What's the Recommendation?

If you have a web application using the implicit flow and all is [hunky dory](https://www.vocabulary.com/dictionary/hunky-dory), then you don't necessarily need to do anything. But for future development you may want to take note of the [OAuth 2.0 Security Best Current Practice](https://tools.ietf.org/html/draft-ietf-oauth-security-topics-13#section-3.1.1) document which states:

> Although PKCE so far was recommended as a mechanism to protect native apps, this advice applies to all kinds of OAuth clients, including web applications.

Basically, it's not that there are new vulnerabilities that have been identified in the implicit flow, just that PKCE offers a more secure alternative that you should use if you have the option. You can find a good, no-nonsense overview of the issues discussed here and solutions in [OAuth2 Implicit Grant and SPA](https://auth0.com/blog/oauth2-implicit-grant-and-spa/) by Vittorio Bertocci.

I hope this overview has been helpful.



