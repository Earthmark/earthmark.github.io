---
title: Modular Homeworld
excerpt: Making a reasonably well built, customizable, homeworld without requiring the user to open an inspector.
---

Making a reasonably well built homeworld customizable, without requiring the user to open an inspector. 

**Status:** Tabled indefinitely, object setup was non trivial, and the homeworld needed more polish than could be provided. The basis tech was repurposed into the ear shard system, where it's still used. 
{: .notice}

The original example homeworld uses a small bootstrap platform, and once a root Homeworld OS instance is inserted the whole rest of the homeworld pops out. 

This runs on the premise that items spawned in Resonite are effectively the same as the world itself, so why not flip it so a homeworld was an item and could have modular pieces.

The homeworld has modular slots that held a totem object of a particular room or area. Removing the totem despawned the contents of the room, and reinserting the totem respawned the contents.

One particularly interesting slot controlled the external area outside of the ”house”, including the skybox and world light.

The project was successful on a technical level, but didn't have any market adoption. The core tech was refined into the Ear Shard system.
