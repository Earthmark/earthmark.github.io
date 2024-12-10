---
title: Light-Reactive 2D Image Baking
excerpt: Originally taught to me by RedDragon, this technique comes up in multiple projects as an optimization for baking a snapshot of a scene into a light-reactive picture for use as a low quality or far away LOD.
---

Originally taught to me by RedDragon, this technique comes up in multiple projects as an optimization for baking a snapshot of a scene into a light-reactive picture for use as a low quality or far away LOD.

The technique:

* Spawn a resonite camera 
  * It should not be moved during this process
  * Capture only targeted should likely be selected
  * Orthographic should likely be selected, but this will depend on use case.
* Pose entities in front of the camera 
  * Once posed, the entities should not be moved. 
  * If the entity is an avatar, turn off the VRIK component to “freeze” the avatar in place. 
* Change the texture of the entities to an unlit variant with the correct albedo
  * All parts of the avatar must be changed
  * The material tool can make this easier by holding a reference to the root of the entities and pressing secondary.
* Take a photo with the camera 
* Change the entities to a world normal matcap 
  * Paste this item link for a pre-configured material
* Take a photo with the camera 
* Create a new PBR material
  * Set alpha to cutout
  * Assign the unit picture to albedo
  * Assign the world normal picture to normal 
* Apply the material to a quad or other flat surface. 
* Wiggle a light around the surface and see it react.

{% capture public-folders %}
The world-space matcap material used:

```
resrec:///G-Earthenworks/R-E793EADA98C714A3B64FF55612742CF744470AA078378E5F3EFC7723AE4161A6
```

**To use a folder link:**
* Copy the link to your clipboard
* Paste the link inside of Resonite, this will spawn an inventory folder link.
* Save the folder link to your inventory
* Spawn the material from the folder.
{% endcapture %}

<div class="notice--primary">
  {{ public-folders | markdownify }}
</div>

The technique is very good for far objects where depth isn't important, low quality LODs for expensive assets (like avatars) or providing “Windows” into other spaces.

# RedDragon Wizardry

RedDragon has a more advanced version of this that prints perspective based light reactive flat-avatars.

The basic technique is the same as is used for other flat avatar bakes (such as used by Creator Jam): 
It works by taking dozens of pictures of a central point with the cameras looking at that point, bakes the prospectives into a tiled maps, and picks the correct tile based on the direction of the user versus the avatar. 

RedDragon modified a version to use the above technique to make the flat avatars light reactive, which dramatically improves realism.
