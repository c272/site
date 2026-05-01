---
layout: post
title: Steam Inventories in NodeJS
date: 2018-01-15
tags:
  - NodeJS
description: >
  A footnote on managing inventories using the Steam API.
coverImage: /img/covers/steam-inventories.png
url: /blog/code/steam-inventories-in-node/
---
{{<notice "alert" "Warning: This article was written in 2018, when the Steam API for inventory management was different. The information here may now be outdated or incorrect.">}}

In NodeJS, the closest you’ll get to indexing is using a dictionary with keys as the name of the object, and data as the contents. This is what Dr. McKay employed when he created node-steamcommunity, and is used in the function that allows you to grab the available inventories of a user, called **getUserInventoryContents()**.

This function usually requires you to use an object from the function `getUserInventoryContexts()`, which returns an array with multiple objects within, containing all the AppID and context data of the user’s available inventories. These objects are extremely awkward to work with, as the documentation currently is quite vague on the structure of the returned object.

The listed structure is set as such:
~~~
appid{??,??,??}
~~~

It mentions that the AppID is the name of the object, however only says that the “context data and game data” is included.

So, when grabbing inventories for a Steam bot, I was running into trouble when trying to get the context ID for app 730, Counter Strike: Global Offensive.

However, I discovered on Dr. McKay’s IPS community forum that the default context ID for all Valve games is 2 [^1], however other games are up to the discretion of the developer in terms of setting context ID.

This leaves most common Steam bot developers in a good situation, as most people programming the bots are using Valve games, as was I. However, anyone wanting to use these commands to get an inventory array for say, BattleBlock Theater or Tower Unite, will have to deal with the undocumented mess that the context function spits out.

So, this is a PSA for anyone looking for context IDs: **2 for Valve, and unknown for anything else.**

[^1]: The link for this post is sadly lost to time.
