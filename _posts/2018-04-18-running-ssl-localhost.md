---
layout: post
title: "Running SSL on localhost"
date: "2018-04-18"
categories:
    - web development
description: Some strategies for local testing with SSL
comments: true
---

Before I get started with the how, I assume some of you may be asking, "Why do I care about running SSL on my localhost?" Well, there are some specific situations that you may care. Here are just a few:

1. You are enforcing SSL in production and want to ensure that you can test for errors that may pop up in production when working locally. For example, errors related to non-secure resources being loaded and causing security warnings or errors related to potentially broken links when redirecting to SSL.
2. You are making an ajax call to an API that uses SSL and are running into a [same origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) error due to the different protocol. This should be solvable via [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) if you control the endpoint, but you may not.
3. You are developing a PWA, which requires SSL. While you should be able to ignore warnings related to SSL for local testing, you may prefer to more closely replicate your production app locally for testing.

There may be others, but these are some that I have run into myself.

Now that we have some reasons _why_ you might want to run your localhost on SSL, let's look at how to do it. In this post, I'll look at some examples when using a simple Node web server, running Jekyll and running Wordpress. All of my examples are running on MacOS. Obviously, there are a ton of other local web server setups that I won't get to cover.

## SSL with localhost on a Node Web Server

For many local web development tasks, I rely on simple HTTP servers built on Node. There are a ton of them available in npm. It turns out that many of them support SSL. One of the options that I have installed, [local-web-server](https://www.npmjs.com/package/local-web-server), even comes with a certificate that you can use to automatically launch localhost on SSL with just a command line option.

```bash
ws --https
```

The problem is that, by default, you'll get this lovely error.

![Not safe error](/images/posts/ssl-localhost/error.png)

You can, of course, proceed to localhost but you won't see the "secure" icon in Chrome, which may obscure other security issues (like insecure resources on a secure page). If you want the secure checkmark, they offer [detailed instructions](https://github.com/lwsjs/local-web-server/wiki/How-to-get-the-%22green-padlock%22-using-the-built-in-certificate) on how to do this for Mac OS.

The instructions generally work for me running MacOS Sierra (yep, I'm still avoiding High Sierra until someone convinces me of a compelling reason to switch). I will note that I could not easily navigate to the installation folder that contains their built-in certificate (in my case, this is `/usr/local/lib/node_modules/local-web-server/node_modules/lws`) from within Keychain Access. Instead, I located it via Finder and then simply dragged the certificate into my "login" keychain.Once you do that, click on it to open it.

![trusting the lws cert](/images/posts/ssl-localhost/trust-lws.png)

Expand the "Trust" section and set "Secure Sockets Layer (SSL)" to "Always Trust."

If you prefer not to use the web server's included certificate but want to use your own, the [instructions](https://github.com/lwsjs/local-web-server/wiki/How-to-get-the-%22green-padlock%22-using-the-built-in-certificate) also demonstrate how to do that, though it wasn't a critical issue for me, personally.

## SSL with localhost with Jekyll

I have used Jekyll to build a number of sites, including [my blog](https://www.remotesynthesis.com/) which enforces SSL. When building Jekyll locally, you'll typically use the built-in web server that builds the pages and allows you to test them in the browser. The good news is that it is fairly easy if you want to do this and test the page locally using SSL.

The first step would be to generate a certificate for your localhost. [This guide](https://letsencrypt.org/docs/certificates-for-localhost/#making-and-trusting-your-own-certificates) from Let's Encrypt offers good instructions that you can just copy/paste into the Terminal.

```bash
openssl req -x509 -out localhost.crt -keyout localhost.key \
  -newkey rsa:2048 -nodes -sha256 \
  -subj '/CN=localhost' -extensions EXT -config <( \
   printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
```

![generating a certificate](/images/posts/ssl-localhost/generate-cert.png)

I placed the generated certificate and key file into a folder named ssl in my documents root. However, as [this issue](https://github.com/jekyll/jekyll/issues/5046) points out, Jekyll's SSL support expects the certificate and key to be inside the site's files. That makes sense, and you could easily just place them there if you like. Since I have a number of projects that would potentially use the same certificate, I didn't do that and instead created a [symlink](http://osxdaily.com/2015/08/06/make-symbolic-links-command-line-mac-os-x/) to the ssl folder in Documents from within the project root.

```bash
ln -s /Users/brinaldi/Documents/ssl /Users/brinaldi/Documents/projects/remotesynth.github.io/ssl
```

As a side note, you'll want to make sure you don't check this symlink in with your project, so you may want to add it to your .gitignore.

Now you can launch the Jekyll server specifying the certificate and key locations using the symlink.

```bash
jekyll serve --ssl-key ssl/localhost.key --ssl-cert ssl/localhost.crt
```

Of course, you'll need to go through the process I discussed earlier to avoid the security warning in Chrome. Drag the certificate into Keychain Access, click on it and then set the "Secure Sockets Layer (SSL)" setting to "Always Trust."

![trusting the localhost certificate](/images/posts/ssl-localhost/localhost-cert.png)

Now you'll get the "Secure" icon.

![secure localhost](/images/posts/ssl-localhost/secure.png)

## SSL with localhost using ngrok

There are a number of other scenarios that I personally run into where I may potentially need to test SSL locally.  For example, Hugo, the other static site server I build locally, does not support SSL via its built-in web server. Or I also still occasionally work on a Wordpress site, which involve going through a [long list of instructions to update the Apache config](https://gist.github.com/jonathantneal/774e4b0b3d4d739cbc53).

A quick and easy solution to this is to use a service like [ngrok](https://ngrok.com/). For basic local testing, the free account should suffice, but it is a paid service if you are looking for more options.

The first step, of course, is to [download ngrok](https://ngrok.com/download). Once you run it, you’ll need to connect it to your ngrok account – the tool will walk you through the process. I find it easier to add ngrok to my PATH variable as well so that I can access it via the command line from anywhere.

Once you are all set up (and assuming you have it on your PATH), you can launch the HTTP port forwarding service. For example, to port forward my built-in Hugo server (which, by default, uses port 1313), I just use the following:

```bash
ngrok http 1313
```

Now I can access the site running locally using SSL via the provided URLs.

![ngrok](/images/posts/ssl-localhost/ngrok.png)

If you're looking for a quick and easy way to test SSL locally, and are ok with signing up for an ngrok account, then this is definitely the simplest option.