---
layout: post
title: "Conforming to JavaScript Code Styles"
date: "2018-03-12"
categories:
    - web development
description: A quick tip on integrating Prettier with ESlint in VS Code.
comments: true
---

In recent years, the code I have written has been mostly solo work, so I have not had to conform to any coding style guide. This can lead to some bad habits. Recently, however, I began contributing some code as part of the [Kinvey](https://www.kinvey.com/) team and needed to conform to their style guide.

Here's the thing though - writing code according to a style guide isn't easy. Taking the [AirBnB JavaScrpt style guide](https://github.com/airbnb/javascript) as an example (which Kinvey's is largely based on), I understand all the rules but following them means breaking a lot of old habits and learning new ones.

For those of you already on teams that follow best practices, these tips may seem obvious. But for those of us making the transition, hopefully this is useful.

## Linting Helps

Fortunately, tools like [ESLint](https://eslint.org/) will tell me where I messed up and didn't follow the style guide. This lets me write code as I normally would, but then clean it up to follow the style guide. Running `eslint --init` will even allow you to configure ESLint to follow some popular style guides beyond the default ESLint recommended styles.

The nice thing is that ESLint let's you [share configurations](https://eslint.org/docs/developer-guide/shareable-configs), allowing the team to all easily abide by the same standard. A lot of teams post their rules publicly including:

* [Google](https://github.com/google/eslint-config-google)
* [AirBnB](https://www.npmjs.com/package/eslint-config-airbnb)
* [Walmart Labs](https://github.com/walmartlabs/eslint-config-walmart)
* [FormidableLabs](https://github.com/FormidableLabs/eslint-config-formidable)

This is great, and once installed, using `eslint --fix` can even automatically fix many problems, but wouldn't it be nice if this just worked in your code editor to let you fix style issues as you code?

## Prettier is Easier

[Prettier](https://prettier.io/) is a code formatter the supports multiple languages and editors, including a [Visual Studio Code extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) (my editor of choice).

Prettier has default styling rules but is configurable. However, since I already have rules defined for ESLint that I want to follow, I can just [configure it to use those](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode#user-content-vscode-specific-settings).

To do this, first click the little gear in the lower-left corner of the editor and choose "Settings".

![VS Code Settings](/images/posts/vscode-settings.png)

Or type `cmd/ctrl+shift+p` and search for "Open user settings".

![VS Code Settings](/images/posts/vscode-usersettings.png)

All of the Prettier default settings are prefixed by `prettier.` if you want to see what they are. However, in this case, I just want to configure a user setting for this project by adding the following line to my Workspace Settings.

```javascript
 "prettier.eslintIntegration": true
 ```

 So that it looks like so (assuming you don't have any other workspace settings).

![VS Code Workspace Settings](/images/posts/vscode-workspace-settings.png)

You can change your user settings if you want this setting to be used across the board in your projects, but this seems more like a project by project type of setting to me.

Now that this is set, I use `cmd/ctrl+shift+p` and search for "Format Code" and it  automatically formats my JavaScript according to the ESLint style guide I configured previously.