---
layout: post
title:  "On the purging of belt balancers"
date:   2018-11-05 23:30:00 -0500
categories: [balancers, blueprints]
factorio_version: 0.16.51
---

During the month of October 2018, the admin at the official Factorio wiki removed the belt balancer compendium. This caused quite a bit of panic on the internets, but ended up being one of those issues that looked larger than it really was.

For those who do not know: what is a belt balancer and why do people care about them?

A belt balancer is a group of belt entities - belts, underneathies, and splitters - that evenly distributes its inputs to its outputs. The wiki [still has a good page on the topic][1] even if the balancer compendium itself was removed.

Great, that page explains what they do. Why should I care?

Until recently, there were three reasons to use them:

1. They draw evenly from the inputs under lopsided load. For example: think of a train station where you have four cargo wagons, each producing one belt of items. To ensure that the wagons unload fairly evenly, use a belt balancer. Otherwise, you risk having some belts empty while others are backed up. This actually reduces overall throughput.

1. They can change the number of belts in a way that makes them even. For example: perhaps you have a mining outpost with six belts of ore, but they are all 2/3 full. You can use a six-to-four belt balancer to _reduce_ the number of belts in a way that draws from all the inputs evenly. This makes the whole ore patch run out slightly sooner, but avoids the situation where ore is slowly trickling into the train's buffer chests near the end of its life.

1. They redistribute items under less than full load. Imagine a [main bus design](https://wiki.factorio.com/Tutorial:Main_bus). Love it or hate it, it is a popular factory design. You tap into the bus and pull items to the side to do things with them: make science packs, gears, atomic bombs, whatever you need. Eventually, resources on the bus start to thin out. A balancer cannot make the belts full again, but it can prevent bus taps from receiving zero items as long as there are items to distribute.

The third reason has been superseded by [priority splitters in version 0.16.17][2]. Priority splitting also allows one to reduce the number of belts, however, it does not do so evenly. Regardless, that removes one reason to use them.

<img src="/assets/belt-taps-compared.png" alt="comparison of belt balancers and priority splitters on a main bus" class="center"/>

The reason I do not care that the balancer compendium was removed is because _most of those balancers were awful_. Easily half of them are useless to begin with. Who needs a one-to-two or two-to-one? That is simply called "a splitter." How many times have I ever used a two-to-seven or eight-to-three balancer? Exactly never.

Some of them are more useful. In the past, I have found myself reaching for a six-to-four quite often, and occasionally an N-to-(N-1) when I need to shave off a belt or two.

However, the real reason they were awful is even if you have a legitimate need for one, the vast majority of them are _throughput limited_. Go back and [reread that first wiki link][1]. A throughput-limited balancer will underperform with uneven load, which happens often enough to matter. Thankfully, there is an easy solution.

**Use throughput-unlimited balancers of size 2<sup>N</sup> and simply leave some of the inputs and outputs unused.** I only ever use these three balancers since the priority splitter change made me reevaluate balancers in general:

* The common four-to-four balancer that is throughput-unlimited, that is, it has splitters on the end.

<img src="/assets/balancer-4-4.png" alt="four-to-four belt balancer" class="center"/>

* Any of the common eight-to-eight balancers. Note that most of the blueprints out there are throughput _limited_. There are three situations for dealing with this.

  * If I absolutely need it to be throughput-unlimited, I duplicate it and feed the first into the second. I actually blueprint down the same blueprint minus the first row of splitters which are redundant in this situation.

<img src="/assets/balancer-8-8-doubled.png" alt="eight-to-eight belt balancer" class="center"/>

  * Loop unused outputs back to the inputs. This usually works for situations where the inputs and outputs are equal in number, e.g. six of each.

<img src="/assets/balancer-8-8-loopback.png" alt="eight-to-eight belt balancer" class="center"/>

  * Do not use all of the inputs and outputs, but spread them out. Ensure that each input splitter is fed by at least one belt, and each output splitter has at least one belt coming from it.

<img src="/assets/balancer-8-8-spread.png" alt="eight-to-eight belt balancer" class="center"/>

* One of the several sixteen-to-sixteen balancers. Some of them are throughput-unlimited, including most of the fractal designs. Those that are not are close enough. I deal with any shortcomings the same way as with the eight-to-eight above.

That is it. I have yet to find a use for anything larger than sixteen-to-sixteen, and anything smaller can be handled quite easily by the previous methods with good results.

Another important point worth mentioning: by the time you reach endgame, balancing is less of an issue because you are building beaconed setups where all the belts are compressed anyway. If there are no gaps in the belts, there is no need to balance most of the time. Limit it to train loading and unloading.

### Conclusion

The more I thought about this, the more I realized that the balancers removed from the wiki are mostly garbage. The few worth salvaging exist on [Factorio Prints][3] already, and they cover any belt balancer use case I can think of. Ever since I rethought my use of belt balancers with the 0.16.17 priority splitter changes, I had already altered my usage enough that I was not using any but three of the balancers anyway.

Meh.

[1]: https://wiki.factorio.com/Balancer_mechanics
[2]: https://wiki.factorio.com/Version_history/0.16.0#0.16.17
[3]: https://www.factorioprints.com/
