---
layout: post
title:  "When does UPS matter?"
date:   2019-01-10 21:00:00 -0500
categories: 
factorio_version: 0.16.51
---

UPS. The hidden resource in Factorio, or so I am told. Bane of megabases and new players' games alike.

Wait, what? That makes no sense, but I see it on the forums and reddit on a regular basis. New players, have not even hit blue science yet on their first playthrough, agonizing over UPS because they read somewhere that UPS is a thing and everyone needs to be concerned about it.

What is UPS? For those who have not been introduced, it simply stands for "updates per second." The game has 60 "ticks" each second, with each tick being one full update of the game state. This means that every second, Factorio updates the position of each inserter, each item on a belt, each train, each spec of pollution, etc. sixty times. That is, unless your UPS goes down.

If your computer cannot complete all of the processing for an individual tick in roughly 1/60th of a second, then you will not have 60 ticks, or updates, per second. There is likely some overhead and between-tick computing that must occur, but conceptually, that is how it works.

When this happens, the entire game slows down. If you have 30 UPS, that means the game simulation is running at half speed. This is different from FPS, or frames per second, which is strictly related to rendering. It is quite possible, and even probable, that if one of the numbers is under 60, the other does not match it exactly. If your GPU is awful but the CPU can keep up, you may have a choppy 30 FPS but the game runs at full speed. If you have a massive factory that stresses the CPU but your GPU can easily handle anything you throw at it, your game may look smooth as butter but run at a slow 30 UPS.

To measure your UPS, press F4 in-game and select the option "show-fps" at the top. This will show both the FPS and UPS in real-time.

That is an explanation of _what_ UPS is. Now I am going to make the controversial stand that UPS largely does not matter.

I see a lot of posts on the [official forums][1] and on [reddit][2] about players trying to be forward-thinking regarding UPS. Many of them are setting up fluid processing for the first time on their way to blue science and talking about optimal pipe layout so as not to harm their UPS.

_Their starter bases will never run into UPS problems_. The real damage here is they are limiting their imagination because they read somewhere about how important UPS _to megabases_. Sure, when you are pushing 5,000 SPM (science per minute) then UPS is an issue. However, only around 0.1% of all Factorio players will _ever_ reach that threshold.

Furthermore, Factorio 0.17 includes many improvements to fluid handling (a major source of UPS pain in large bases) and 0.16 already made massive improvements to belt UPS. I dare say that in 0.17, UPS will have even less of an impact even on smaller megabases. At some point there is simply too much going on for the CPU to do it all in 1/60th of a second, but Wube seems intent on optimizing the game as much as possible to appease the megabase builders. This is a good thing, because it makes this irrelevant topic even more irrelevant.

If you are worried about UPS, do not be. Let your imagination run wild and have fun with the game. If you ever get to the point that UPS matters, you are already planning a megabase and have the experience to know what to do. Until then, free your mind of worries and have fun!

[1]: https://forums.factorio.com/
[2]: https://www.reddit.com/r/factorio/
