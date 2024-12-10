---
title: Relative Root
excerpt: A system for bypassing distance from root issues, allowing for functionally infinite maps; provides a lot of conditions are met.
---

A system for bypassing distance from root issues, allowing for functionally infinite maps; provides a lot of conditions are met.

The system has a virtual Root space where all children under it have a virtual transform that additionally contains a uint3 of what chunk in 3d space the virtual transform occupies. As a transform moves out of one chunk, the float3 position coordinate wraps to the be back within range, and the chunk index is updated appropriately.

The local users chunk index is broadcast as a dynamic variable, and all virtual entities only render themselves if they are within a certain number of chunks of the root user. The logic to project a virtual transform is in every virtual entity.
Gotchas
Users used to not be able to get too far from each other or they will delete each other. To get around this there is a staging position at origin (which is in the center of whichever chunk the local user currently occupies) that contains every other not currently visible chunk.

This system looks like garbage in a lot of cases, if a user has a particle trail it's very possible the trail will suddenly jump at chunk barriers.

Headless servers generally need to have every user active and not hidden at the same time or strange behaviors come up. As all users will generally be overlapping in this case issues like users grabbing each other, or items off each other, accidentally out of one space into another can come up.
