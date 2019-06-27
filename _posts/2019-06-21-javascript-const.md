---
layout: post
title: Confused by JavaScript's const? Me too!
date: '2019-06-21'
description: Constants in JavaScript don't necessarily behave the way you think they would.
categories:
  - javascript
  - web development
comments: true
---

The other day I had a little back and forth on Twitter around the concept of `const` in JavaScript. Kyle Simpson had pointed out a misunderstanding around `const` within an article I'd shared. My sentiment was, more or less, that I can understand where the confusion comes from since it often feels that `const` doesn't behave the way I'd _expect_ it to (note, I'm not saying it is wrong, just different from my expectation).

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr">Hmm... I missed this issue when I read this article. But if he (and many others) misunderstands &#39;const&#39;, could it be partly because &#39;const&#39; frequently doesn&#39;t behave the way you think it would.</p>&mdash; Brian Rinaldi (@remotesynth) <a href="https://twitter.com/remotesynth/status/1138084777674924034?ref_src=twsrc%5Etfw">June 10, 2019</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Even in that brief conversation, a lot of terminology and concepts were thrown around. So I thought, let me dig into this a bit so I can better understand the concept of constants and the ways in which a variable declared with `const` actually works in JavaScript.

> I should note that Kyle Simpson did write a post on this very topic, but it appears to be on a blog that is no longer live. He did share the [version available via the Wayback Machine](https://web.archive.org/web/20151113135159/http://blog.getify.com/constantly-confusing-const). It's worth a read as he goes into far more depth than I plan to.

## What is a Constant?

If you Google "What is a constant in programming?", you'll find numerous pages that generally define a constant in the way it is defined on [Wikipedia](https://en.wikipedia.org/wiki/Constant_(computer_programming)) as a "value that cannot be altered by the program during normal execution."

On the surface, this seems rather simple - set a value and it cannot be changed. This can be useful for both readability and error checking. However, not all languages have constants, and those that do don't always handle them the same. For example, in some languages the types of values a constant can hold are limited.

It's once you get beyond the simple value types where things can get confusing. This is important to the conversation here (and where a lot of my own confusion around the expectation versus the reality of constants in JavaScript comes in). Rather than try to explain, I'll give an example.

Let's say I set a constant like so:

```JavaScript
const NAME = "Brian";
```

It seems obvious that trying to assign any new value to `NAME` will result in an error - and it does. But what if I did the following:

```JavaScript
const ME = {name:'Brian'};
```

If I change the value of `ME.name`, should I get an error? One could argue that technically, I am not changing the value of `ME` since it is still pointing at that same object, even though that object has been mutated. To be clear, in JavaScript, this will _not_ give you an error.

![changing the value of an object constant](/images/posts/const_object.png)

It's at this point that computer science folks will get into the concepts of primitives and immutability. We'll talk a bit about these but, for the sake of not turning this into a chapter in a computer science book, I'm not going to cover them in great depth.

> In brief, an immutable object is an object whose state cannot be modified after it is created. A primitive in JavaScript is "data that is not an object and has no methods." (source: [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Primitive))

## Constants in JavaScript

The `const` keyword was added to JavaScript in ES6 (aka ES2015). Previously, the common convention was to use a standard variable but with an all-caps name like `MY_CONSTANT`. This didn’t effect whether the variable could be changed - it was more a hint to tell developers that it shouldn’t be changed.

JavaScript constants declared with `const` can either be global scoped or block scoped. If they are within a block (i.e. between `{` and `}`) they are automatically block scoped. If they are not within a block, they are global scoped, but, unlike variables declared with `var`, do not become properties of the window object. Basically, the scope of a `const`-declared variable is always the innermost enclosing block. In case of a script, it is the global scope or, in case of a module, it is the scope of that module. (Hat tip to [Axel](https://twitter.com/rauschma) for the clarification.)

Another interesting difference between `const` and `var` is that they are [hoisted](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting) differently. When you declare a variable using `const` or `let`, the declaration is hoisted, but its value is not initialized as `undefined`, thus you will get a reference error if you try to access it prior to the declaration. As you can see below, the first `console.log` referencing a variable defined with `var` returns `undefined` but the second using `const` generates an error.

![temporal dead zone](/images/posts/reference_error.png)

This is referred to as the [temporal dead zone](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone), which makes it sound much more ominous than it is.

The final important thing to note about `const` in JavaScript is, as discussed earlier:

> The const *declaration* creates a read-only reference to a value. It does *not* mean the value it holds is immutable, just that the variable identifier cannot be reassigned. ([source](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const))

Again, this is where the confusion around `const` seems to emanate from. If you are using `const` with [JavaScript primitive types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Primitive_values) (i.e. boolean, number, string, etc.), it'll behave the way you might expect (any reassignment generates an error). But, when using `const` with [JavaScript objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Objects) (including arrays, functions, etc.), that object is still mutable, meaning properties of that object can still be changed.

For a more detailed look at scoping around `let` and `const`, there is a whole chapter in "[JavaScript for Impatient Programmers](https://exploringjs.com/impatient-js/ch_variables-assignment.html#const)" on `let` and `const` by Axel Rauschmayer.

## Should You Use Const?

This is a tough question to answer, especially because `let` has the same benefits of block scoping and hoisting (and I cite the latter as a potential benefit since the way `var` is hoisted could lead to unusual errors whereby a variable is inadvertently accessed before it is declared). The people who tout the benefits of `const` then typically focus on code readability. By using `const`, you have indicated that this specific variable should not change, and it will enforce that to a certain degree.

The argument for `const`'s readability, though, is a bit undercut by the fact that people seem to regularly misunderstand it, as we noted at the start of this article. Yes, there are some protections against reassigning this variable, but, to quote [Kyle's article](https://web.archive.org/web/20151113135159/http://blog.getify.com/constantly-confusing-const):

> Actually, many developers assert this protection keeps you from having some unsuspecting developer accidentally change a `const`. Except, in reality, I think the likelihood is that a developer who needs to change a variable and gets a const-thrown error about it will probably just change the `const` to `let` and go on about their business.

So, if the protections `const` provides are minimal, it simply becomes a matter of style preference, particularly when choosing between `let` and `const`. If your variable will hold a primitive value that is not intended to be changed, sure, using `const` is a reasonable choice. However, recognize that if the value is something other than a primitive value, using `const` could potentially be more confusing, from a readability perspective, than helpful.
