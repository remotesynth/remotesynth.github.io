---
layout: post
title: "Update Fails on ffi Install in Ruby"
date: "2017-04-21"
categories:
    - static sites
description: Saving you the headaches I had.
comments: true
---

File this one as a niche issue, but in case someone else ends up losing a morning to this issue, I figured I'd post it.

I was trying to update my blog to a newer version of Jekyll. However, my attempts at running `bundle update` kept running into this error:

```bash
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

current directory: /usr/local/lib/ruby/gems/2.3.0/gems/ffi-1.9.18/ext/ffi_c
/usr/local/opt/ruby/bin/ruby -r ./siteconf20170421-40871-1dh28zu.rb extconf.rb
checking for ffi.h... *** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

...

/usr/local/Cellar/ruby/2.3.1/lib/ruby/2.3.0/mkmf.rb:456:in 'try_do': The
compiler failed to generate an executable file. (RuntimeError)
You have to install development tools first.

...

Make sure that \`gem install ffi -v '1.9.18'\` succeeds before bundling.
```

Trying to run the suggested `gem install ffi -v '1.9.18'` failed as well. The actual solution is in the error but isn't necessarily obvious. They key is this part: `You have to install development tools first.` I'm on a Mac, so that means XCode. However, just going to the App Store and getting XCode isn't enough, the key is in step 2 below.

1. Install XCode
1. _Open XCode_
1. `bundle update`

I should note that after I did all this, I was still getting warnings when I ran Jekyll.

```bash
Unresolved specs during Gem::Specification.reset:
      rb-inotify (>= 0.9.7, ~> 0.9)
```

These went away after running a `gem cleanup`.

Lastly, I was getting a bunch of additional warnings like the following:

```bash
warning: already initialized constant JSON::VERSION
```

These went away after running `bundle clean --force` and then rerunning `bundle update`.

This may seem obvious to some of you (especially those more comfortable in the Ruby environment), but I found a ton of people with similar problems (some specific to Jekyll, others to different Ruby gems), so I figured I'd post it.