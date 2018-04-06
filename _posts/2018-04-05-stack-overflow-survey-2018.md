---
layout: post
title: "Some Things You May Have Missed in the Stack Overflow Developer Survey"
date: "2018-04-05"
categories:
    - general
description: Let's dig into the data a little bit.
comments: true
---

Yeah, I know what you are thinking, "The [Stack Overflow Survey](https://insights.stackoverflow.com/survey/2018/) was last month's news!" True. But there was so much data to digest in there that, honestly, it takes a lot of time to process. This meant that many of the early posts focused on headline info, like the [most loved/dreaded/wanted languages](https://insights.stackoverflow.com/survey/2018/#most-loved-dreaded-and-wanted). Now that I've had a little bit of time to sift through all the information, I wanted to share some things that struck me as important, even if they didn't necessarily catch the biggest headlines.

I should note that in all cases below, when I refer to developers, I mean respondents. Obviously, even though over 100,000 people took the survey, it probably has some bias due to the fact that it is [heavily tilted towards at least somewhat regular StackOverflow users](https://insights.stackoverflow.com/survey/2018/#community-visiting-stack-overflow).

## We are not diverse - like, at all!

The demographics section overall was disappointing overall. This isn't helped by the fact that a substantial number of developers [don't think diversity is a priority](https://insights.stackoverflow.com/survey/2018/#work-how-do-developers-assess-potential-jobs) (including both [men and, surprisingly, women](https://insights.stackoverflow.com/survey/2018/#work-differences-in-assessing-jobs-by-gender). The net result is that the prototypical developer is a white, male under the age of 35 with no children.

### We are almost all men

Developers are, sadly, a very homogenous group - almost [93% male](https://insights.stackoverflow.com/survey/2018/#developer-profile-gender), over [74% white](https://insights.stackoverflow.com/survey/2018/#developer-profile-race-and-ethnicity), and over [93% straight](https://insights.stackoverflow.com/survey/2018/#developer-profile-sexual-orientation). Compare that to the general population that is obviously slightly over 50% female.

And all the diversity efforts to bring more women into the industry doesn't appear to be changing things in any real noticeable fashion. Looking at just students, the numbers shift by less than a percent. The only potential bright spot is that [women represent a growing share of developers with less than 5 years experience](https://insights.stackoverflow.com/survey/2018/#developer-profile-experience-and-gender).

### We are mostly white

The racial breakdown is especially disappointing since, <strike>as best I can guesstimate, only a [bit more than 50% of the respondents are from North America and Europe](https://insights.stackoverflow.com/survey/2018/#geography)</strike> [63% of the respondents are from North America and Europe](https://insights.stackoverflow.com/survey/2018/#methodology). Nonetheless, over 74% of all developers identify as white or of European descent. The geographic breakdown leads one the conclusion that, in North America and Europe, the breakdown would be significantly more white than the overall percentage. This bears out in the commentary, which notes that "7.4% of professional developers in the United States identified as black, Hispanic or Latino/Latina, or Native American" compared to over 30% of all respondents. On a positive note, this number improves slightly when reducing to only students - so change is happening in this area, but very slowly.

### We are mostly young, without children

Almost [73% of developers are under the age of 35](https://insights.stackoverflow.com/survey/2018/#developer-profile-age). Personally, I am on the cusp of falling into the 45 or older category, which represents slightly less than 7% of developers - and I can attest to my age already coming up at most every developer event I have attended over the past 5 years. Slightly more than [71% have no kids](https://insights.stackoverflow.com/survey/2018/#developer-profile-children-and-other-dependents), which matches pretty closely with the under 35 category.

## Web technologies rule everything...

### ..but the paycheck 

JavaScript, HTML and CSS rule the [top languages used by developers](https://insights.stackoverflow.com/survey/2018/#technology-programming-scripting-and-markup-languages) making up more than two-thirds of respondents, with JavaScript being the most prevalent of the three (the numbers even go up slightly for all three when filtered for just professional developers). Also, a [combined 64% are using either Angular or React](https://insights.stackoverflow.com/survey/2018/#technology-frameworks-libraries-and-tools) (with Angular showing up as modestly bigger) and almost 50% say they are using Node.js.

However, popularity doesn't translate into pay. Web technologies are at the [bottom of the pay scale](https://insights.stackoverflow.com/survey/2018/#technology-what-languages-are-associated-with-the-highest-salaries-worldwide) (both globally and in the US where only JavaScript makes the list at second to last). If you want to make money, it appears to be in the less widely used back-end languages like Erlang, Scala, Ocaml and F#. Front-end developer as a title sits somewhere in the middle of the [salary stack](https://insights.stackoverflow.com/survey/2018/#salary) overall.

### Mobile is still a (large) niche

The [native mobile contingent](https://insights.stackoverflow.com/survey/2018/#technology-programming-scripting-and-markup-languages) wasn't quite as large as I expected. Swift is at 8.3% and Objective-C is still at 7.3%, which, when keeping in mind that this category allows overlap, means that very likely less than 10% overall are doing iOS development (which would fit with the [XCode numbers](https://insights.stackoverflow.com/survey/2018/#technology-most-popular-development-environments) which sit around only 10% and the [correlated technologies](https://insights.stackoverflow.com/survey/2018/#correlated-technologies) section shows there is indeed some overlap), although 15% did say that they are developing for iOS as a platform overall. Android isn't broken out of Java in the languages section, but the [IDE section](https://insights.stackoverflow.com/survey/2018/#technology-most-popular-development-environments) shows Android Studio at 19.3% and platforms show it at 29%, which is a bit unusual given the dearth of native iOS developers. Since well over 50% of respondents doing mobile were doing Android, I wonder if there might be a bit of a Java/Android bias to the StackOverflow audience.

Other mobile-focused development technologies were also relatively small, with Xamarin and Cordova showing a combined 15% (since I'd assume minimal overlap between the two). Tools like React Native or NativeScript did not make the list. Unfortunately, for Xamarin and Cordova is that they also both [top the most dreaded tools/frameworks list](https://insights.stackoverflow.com/survey/2018/#technology-most-loved-dreaded-and-wanted-languages).

### Back-end development is all over the place

Java is still the king when it comes to back-end development, but Python and C# are not that far behind. A lot of people (31%) still do PHP, and it isn't just Wordpress (less than 16% use WordPress). Significant numbers of developers do C and/or C++ while small but not insignificant percentages do Ruby and Go. The numbers would indicate that many developers work with multiple back-end languages.

### Rust and Kotlin developers really love their languages

Rust and Kotlin developers are clearly a small but passionate group. Rust didn't even make the language list and Kotlin came in at only 4.5%, but they significantly outpace most ever language in terms of the developers who use it [wanting to continue working with it](https://insights.stackoverflow.com/survey/2018/#most-loved-dreaded-and-wanted). Rust knowledge is fairly high up on the [global pay scale](https://insights.stackoverflow.com/survey/2018/#technology-what-languages-are-associated-with-the-highest-salaries-worldwide), so perhaps that is a factor.

Overall, developers generally want to learn Python or JavaScript/TypeScript and want to get away from some older .NET technologies in particular. However, both Python and JavaScript are among the lowest paying languages.

## Developers generally like their jobs

This is a [bright spot](https://insights.stackoverflow.com/survey/2018/#work-how-do-developers-feel-about-their-careers-and-jobs). Over 70% of developers are at least slightly satisfied with their career with a majority (55%) moderately or extremely satisfied. Those numbers are essentially unchanged in terms of satisfaction with their current job. However, a significant number of developers [changed their job in the last year](https://insights.stackoverflow.com/survey/2018/#work-how-long-ago-did-developers-last-change-jobs) and a majority (56%) within the last two years. So, perhaps that job satisfaction number is ephemeral.

Perhaps part of the reason developers are happy is that the job pays well overall. Even the lowest paid [category in salary by developer type](https://insights.stackoverflow.com/survey/2018/#work-salary-by-developer-type) in the U.S. is paid about $20k more than the [average salary of a person with a four-year college degree](https://smartasset.com/retirement/the-average-salary-by-education-level) even though just about [75% of professional developers have a college degree](https://insights.stackoverflow.com/survey/2018/#developer-profile-educational-attainment).
