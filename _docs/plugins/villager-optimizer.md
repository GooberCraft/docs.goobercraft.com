---
layout: default
title: Villager Optimizer Plugin
parent: Plugins & Tools
nav_order: 2
permalink: /docs/plugins/villager-optimizer/
last_modified_at: 2025-11-02
---

## The Plugin

We make use of the [VIllagerOptimizer](https://modrinth.com/plugin/villageroptimizer) plugin on GooberCraft. This is a highly configurable plugin with a lot of different approaches. Below are the details you may need to know.

## The Config

### Optimization Method

The plugin provides 4 different methodologies of optimizing a villager. To keep things simple and easily controllable, we have decided on the "Name Tag" method. To optimize a villager, rename a nametag with one of the four following names: `optimize`, `optimized`, `AIDisabled`, or `DisableAI`. You can also obtain a free one by running the command `/kit optimize`. You then apply the nametag to the villagers you wish to optimize. The nametag will not be consumed on use.

### Optimized Attributes

- The pathing AI is completely removed
- Their restocks are on a 2 minute timer
- They can be targeted and attacked by entities _(All other damage prevented)_
  - Being zombified will unoptimize a villager
- A villager can only be optimized every 60 seconds
- Do not apply an optimized nametag unless you plan to keep the villager
  - You can still preview their trades prior to optimizing

At some point, ONLY optimized villagers will be able to be traded with. We suggest you optimize them as soon as reasonably possible.

### Culling

While it is not enabled at this time, villager culling will be enabled at some point in the future.

- Upoptimized Villagers
  - Limit: 20 Per Chunk
- Optimized Villagers
  - Limit: 60 Per Chunk

Culling will be triggered every 60 second with a limit of rechecking every 15 seconds.

The villagers will be culled by this job priority order (first to last):

- NONE
- NITWIT
- SHEPHERD
- FISHERMAN
- BUTCHER
- CARTOGRAPHER
- LEATHERWORKER
- FLETCHER
- MASON
- FARMER
- ARMORER
- TOOLSMITH
- WEAPONSMITH
- CLERIC
- LIBRARIAN

## The Questions

### Q: Do I have to optimize _ALL_ of my villagers?

No, you do not have to optimize all of your villagers, but we ask you optimize as many as you reasonably can. The easiest ones to take care of will be villagers in villager trading halls. The villagers used for the various farms may not be able to be optimized in order to keep the farms functional.

### Q: Can I unoptimize a villager?

Yes, you can un-optimize a villager, just use a different nametag and apply a different name.

### Q: I zombify my villagers and then cure them for discounted trades. Is there anything I need to know?

A: When an optimized villager becomes zombified, they become unoptimized. You'll have to reapply the Optimize tag to reoptimized them.
