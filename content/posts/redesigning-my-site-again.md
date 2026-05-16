---
title: "Redesigning My Site (Again)"
date: 2026-05-16T19:13:38+09:00
description: >
  Efficiently packing booleans to save space I didn't need to.
coverImage: /img/covers/redesigning-my-site-again.png
tags:
  - Hugo
---

A few months ago, I decided to redesign my personal site again, after previously [unifying the design](/blog/code/the-great-blog-migration) of the various (mostly inactive) blogs I was operating in 2023. Here, I want to discuss a little of the motivation behind rebuilding from scratch, and the process it took to get here.

## Why a full rewrite?

Since I had an existing custom theme, *coffeeline*, it may seem a strange decision to rip everything down and build from scratch. There were a few factors involved, but the largest (by far) is simply that the content I want to display on my site has drastically changed in the last three years.

At the point of unifying my blogs, I was in my penultimate year of university and in the throes of a job search, which unfortunately resulted in the landing page for my site becoming a defacto CV. Now gainfully employed (in this economy!) and out of university, this makes little sense. I want people to see the things I'm writing, not an executive summary of my very short career.

One other factor is the state of my prior custom theme. The 2023 site design is a hackjob consisting of an existing open-source Hexo theme, bits and pieces adopted from other blog designs, and a heap of small hacks and shortcodes to achieve a consistent look across the set of existing posts. Put bluntly, it was a mess.

Finally, I am just a different person with different tastes to the university student of three years ago. Serif fonts, monochrome theming and cutthroat minimalism don't appeal to me in the same way they did before, and that should be reflected in my site's design. It's a personal site, after all; they should look like their owners!

With a complete rewrite, I could tailor the site to my personal tastes, while also cleaning up the codebase so my gigantic infrastructure house of cards doesn't collapse under a gentle breeze.

## Goals

I had a few large goals in mind for my complete redesign, so I'll quickly list them off here.

- **No Javascript**
  * "NoJS" has become more of a common sentiment in the online space nowadays, but I wanted my site to function perfectly without the use of scripts. There wasn't much load-bearing JavaScript before, but now there is none at all.
- **One Unified Stream**
  * This is less of a design feature and more of a structural issue, but my blog was previously split into "Code", "Language", and "JP". I don't output remotely enough to justify the distinction, so with the redesign my goal was to unify these all under one "posts" section.
- **Easily Hackable**
  * I am not a web developer, nor a fan of tinkering with HTML/CSS, so one goal was to make the site very easily hackable. If I have an idea for a new page or shortcode, it should be quick to spin up and painless to integrate.
- **Notes**
  * One of my great weaknesses (perhaps this is a universal thing?) is that creating anything substantial to a satisfying quality takes me an inordinate amount of time. To combat this a little, I wanted a section where I could just throw little ideas or things I'm thinking about, without the (self-imposed) pressure of a longer "post".

## The Big Redesign

The redesign itself was relatively quick and painless, but ended up being spread over a period of early April to late May, mostly due to a lack of time investment.

Upon upgrading everything to the newest version of Hugo, it became apparent that my previous Sass setup was entirely broken, so I took the opportunity to switch my site's styling entirely to [Tailwind](https://tailwindcss.com/). It's a system I've become quite fond of over the past few years for its ease of use and hackability for my personal projects, and plays really nicely with editor auto-complete if everything is functioning properly.

Starting from the husk of my previous design, with the boost from Tailwind and keeping everything relatively simple, I finished up the rest of the site's skeleton within a few weekends. Most of the core assets were moved to be entirely locally hosted (such as the primary site font), and all SEO elements were entirely stripped from the design. Let's take a quick look at each of the redesigned pages individually!

![Redesigned List Page](/img/posts/redesigning-my-site-again/list-page.png)
{{% img-caption "The redesigned post list view." %}}

The list pages I wanted to look like one large timeline, with the topmost "node" being the latest post in a series of posts. This was a bit tricky to pull off while keeping a cookie-cutter template for every single post overview, but I think it ended up looking decent enough.

You can also see the redesigned page header here, which takes less space on the page. The design includes more text now, instead of using icons for certain links, which I much prefer.

![Redesigned List Page](/img/posts/redesigning-my-site-again/post-page.png)
{{% img-caption "The redesigned post page." %}}

If you ignore the serif font and the introduction of some colour, the new post design really does not depart much from the existing layout. That's mostly because it was already quite a simple and straightforward design, which I tried to as design principles, however there are a few obvious differences. Tags now appear below the title and date lines for some better visual heirarchy, and links are much more obvious on the page compared to a barely distinguishable grey in the prior design (not sure what I was thinking there).

Overall, I'm quite happy with how the redesign turned out. It mostly achieves what I envisioned prior to writing everything out as HTML/CSS, and does so without being a huge complex mess, which is an important distinction given my last custom theme. There are a few points which I still want to improve upon, however, so let's go over those briefly now.

## Things For The Future

Having reached the line of being good enough to "just ship it", there are of course a few things which I'd like to add in the future that didn't make the cut this time round.

One major one is comments, which were also missing from my previous unified site design, but were present back when I was using a standard Hexo theme for my main programming blog. My experience with Disqus and other similar comment systems has been far from positive, though, so I'm still in search of a sane system to use without going fully non-static. I've seen several others using GitHub discussions as a host with an open source UI layer on top, but that doesn't quite sit right with me either. It's something that needs looking into, but that I haven't had the time or bandwidth to dedicate towards.

Dark mode is another big "nice to have" feature, and one I've at least laid the groundwork for in the redesign. Tailwind has a built-in method of specifying separate dark/light theme colours, which in combination with the custom palette used for the new design, should give me the ability to swap between two palettes seamlessly. This will obviously require JavaScript, however, so will remain non-intrusive & optional.

## Another Redesign?

Having said much about the ethos behind this rewrite and why I've made one decision over another, this will all most likely be another temporary step in a never-ending series of rejigs and design changes to my site, as with the prior N times.

And that's fine. I like tinkering with things, and this is one of the few spaces in which I have complete freedom to do so. These posts let me document each step in the tinkering process, without having to wade through repository histories and old dependencies.

So, until next time!
