---
title: "The Great Blog Migration"
date: 2023-06-21T18:31:15+01:00
tags:
  - Hugo
  - SASS
coverImage: /img/covers/blog-migration.png
url: /blog/code/the-great-blog-migration/
---

Hello! If you're viewing this site after 21st June, 2023, you may notice that the design of this site has changed. In fact, if you're viewing any of my blogs, you may notice that they have **all** changed, be it my programming blog, *Gengo! 言語* or *脇道の看板*. To explain why this all happened in the first place, I'll present a little bit of backstory.

## The Backstory
I've run several different blogs for several different purposes for quite a number of years. First came my programming blog, which has always been on the apex domain of the site you're currently on, [c272.org](/). From 2016 onwards, I continued to (infrequently) update the site and its design up until late 2018, adding posts about various programming projects I was working on at the time, and creating a fair few cringeworthy articles, which have thankfully been lost to time.

Fast forward three years, however, and I wanted to start writing about topics other than programming on my site. One large factor in this was that I began learning Japanese and eventually decided to take on the JLPT N1, which motivated me to write about some of the interesting topics I had come across in my language learning process. However, I wasn't about to suddenly start posting completely unrelated content onto my main blog, which had (up until this point) been entirely programming focused. Also, I wanted to start writing Japanese language content, which obviously wouldn't fly in the same post feed as English language programming articles.

So, in pursuit of this, over the course of several months and different iterations, I set up *Gengo! 言語*, originally at [c272.org/gengo](/blog/language), which ran on Hexo and deployed quite nicely over Github Actions. This hosted all of my language learning content, and was running on a modified version of "Frame" by [zoeingwingkei](https://github.com/zoeingwingkei).

![Screenshot of 'c272.org/gengo'.](/img/posts/blog-migration/gengo-original.png)
{{<img-caption "*Gengo! 言語* captured on 21/06/23.">}}

Later on, for my Japanese language content, I set up *脇道の看板* hosted at [ura.c272.org](/blog/jp), which was running on Jekyll with a custom theme created for the site, again using Github Actions for deployment.

You may be able to see my dilemma at this point -- I had too many dependency stacks, in too many places, with barely any consistency. If someone wanted to view my writing as a whole, they would have to somehow discern three separate, unrelated domain patterns (that being the root domain, */gengo* and the subdomain *ura*). In addition, these blogs also had near zero crosslinking, and no visual consistency. Even still, that wouldn't probably have been enough to convince me to rewrite my entire blogging stack on its own.

What was, however, was the backend maintenance. Even when using Github Actions for deployment and having everything on a static Pages host, which is a pretty easy ask, having to hop around managing dependency stacks for three separate blog systems (Hugo, Hexo and Jekyll) was quickly becoming a bit of a nightmare. Themes breaking, dependencies shaking, all things you really don't want to deal with when you just want to publish a new post. Another pet peeve of mine was that all of their post formatting and frontmatter formats differed very slightly in ways that made them annoyingly non cross-compatible. So, I decided to look for a solution.

## The Solution
I had three core goals which I wanted to achieve when combining my blogs, which were:
- No ridiculous dependency stack management. One system, one package manager.
- Keep the clear separation of different content stacks, to avoid confusion.
- Allow viewers to easily navigate between different stacks of content, with visual consistency.

Unfortunately, simply shifting all of my blogs to use one of my existing systems couldn't fulfill all three of these needs. None of the static site systems I was using offered proper content stack separation apart from Hugo, however the modified theme I was using with it had zero support for that functionality, and was simply designed for a single long stream of content.

Knowing this, I made the decision to rewrite my site anew, fully custom, and offering the functionality I needed for my use case. The choice of system was at least clear -- Hugo was the optimal choice for separating my content effectively. Bonus points for running on Go too -- I can escape Javascript and `npm` at the same time! Two birds with one stone.

This isn't to say I wanted to just throw out the entirety of what I'd worked on previously, though. The plan was to keep some visual elements from my existing blog themes, and combine them into one visually consistent model, with simple and consistent path separation between blogs. Here's what ended up as the final design for the site, although I may do some further minor tweaking.

![](/img/posts/blog-migration/gengo-comparison.png)
{{<img-caption "A comparison of the old *Gengo! 言語* stack and the current, live one.">}}

![](/img/posts/blog-migration/wakimichi-comparison.png)
{{<img-caption "A comparison of the old *脇道の看板* stack and the current, live one.">}}

Personally, I'm pretty pleased with the result. There are still some things that aren't present on the new site that were on the old ones. For example, Disqus comment integration and the archive pages, for starters. However, those are things that I can easily implement in the future on a clean, single codebase, and there are plenty of things that aren't clear externally that have been made far cleaner internally (e.g. the merging of all the shortcodes duplicated across blogs, and unified templating and partials for every blog).

What do you think of the new design compared to the old one? If you have any thoughts, please leave a comment (if I've bothered to set up that system yet), or send me a ping at any of my [contact addresses](/about). Happy reading!
