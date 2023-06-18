---
layout: post
title: To Clip, or Not To Clip
date: 2018-06-16
tags:
  - CS:GO
  - Hammer
description: >
  A collision dilemma, told through CS:GO.
coverImage: /img/covers/csgo_smoothstairs.gif
---

We all have the same issue; Should I clip all my props? Won’t it make players annoyed and cause frustration when something that looks like it should be wallbang enabled/walkable is not?

The answer to the first: Yes.
The answer to the second: Yes.

There’s a compromise to be made here, one that a lot of mappers struggle to find a balance between. For a great example, look at Valve’s maps, especially fine polished ones such as Dust2. These take a more balanced approach to clipping, as well as employing some clever techniques to make the clipping as smooth and unnoticeable for the player as possible, such as at the stairs leading to B as seen in the cover image of this post.

This isn’t without it’s issues, obviously, so don’t take these to be the holy grail of proper clipping, as you can still get stuck at specific points on the map, but it’s a good general practice to follow. The two easy ones are as follows:

- Clip areas that need to be smoothed out.
- Clip areas where the bomb could get stuck, such as in small corners or areas behind crates.

However, a more contentious example would perhaps be the idea of:

- Clip areas that the player isn’t meant to reach.

You may think that this is extremely simple, but in reality it can be a major sticking point for players. The reasoning behind this is, as mentioned before, if it **looks** like you should be able to go to an area, at least one player will attempt it. This is something more prominent map makers have had trouble with too, 3kliksphilip more recently having issues with this in his “de_sparity” map, in which a platform looked like it should have been accessible, which eventually marked down his map. [How unfortunate.](https://www.youtube.com/watch?v=Up3f8ePGcLw&t=626s)

It’s even present on Valve’s own map, Canals, in which a knee high fence prevents you from walking further, seen in the below image.

![img](/img/posts/csgo-clipping/canals.jpg)

Fixing this is more difficult on different maps, such as situations where you can’t just stick in a massive wall, which I’m assuming was the reason for de_canals’ suspiciously absent barriers.

To conclude, you *should* clip everything to keep the gameplay smooth for the player, and avoid exploits such as boosting and bomb stuck spots, but only when it makes sense for your map. Don’t go adding a clipping wall over a 32 unit high box. It’s all really common stuff, but it takes a lot of work to get right, as evident in the Valve maps that have been worked on for years on end that still aren’t perfect.

Happy clipping.