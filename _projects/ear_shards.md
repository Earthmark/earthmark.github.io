---
title: Ear Shards
excerpt: Customizing avatars with additional behaviors on demand, instead of making a single massive avatar.
---

Many variants of this system exist, this is just my (Earthmark's) version of it.

**Status:** Actively used by Earthmark as their avatar config system. Many systems with similar goals have been made, each with pros and cons.
{: .notice}

Ear shards are totem-like objects that attach to snappers on a parent object. When attached, the shard inserts logic and objects into the parent object. When the shard is removed, the custom objects and behaviors are also removed.

They're named ear shards because the anchors were on Earthmarks ears originally, this isn't suggested as trying to grab the shards when you can't see them is frustrating, although personal mirrors make this easier. Currently they are anchored underneath the avatars forearm, similar to the feathers on an Avali

Shards are currently used mostly on avatars, but they can be used on any kind of object such as vehicles or worlds.
Gotchas that came up during this project:
Dynamic bones
Movement of dynamic bones is heavily influenced based on the direct slot ancestors, bypassing the virtual parent component. 

This was discovered when using a shard to allow an avatar to support mature content without needing to put the content on the avatar itself, this allows the avatar to be TOS compliant, but can be used with mature content should it be permitted in the world.

**Grumpy tangent:** The TOS requires mature content not be in public worlds, even if inactive, because the content is still transferred to connecting users who may be non consenting to being provided that content, or even worse underage. Systems that just hide mature content in non-allowing worlds are NOT TOS compliant and you may get reported for using that kind of a system in a public world.
Do not try to be tricky about this and make url swappers or such. They all have failure modes that either may show mature content in the world browser, or may show up for a moment, still transferring content to connecting users. The only safe way is to either have fully separate avatars, or store the content on a separate object that you must explicitly spawn out in allowing worlds.
That being said, try to make the anchor slots not too explicitly named.
PS: The non-mature version of some avatars still contain mature textures, even if they're in a horrific uv unwrapped form.
{: .notice--warning}

Originally the shard used virtual parents, but when the shard was parented to the avatars ear the movement of the avatars head and neck was automatically applied to the virtually parented mature object. This looked hilarious, but detracted from the intended effect.

For this reason shards should generally instance content into the parent object instead of virtual parenting.

Driving Dynamic Variables
Dynamic variables are used to identify slots where instances should be parented, and to get data out of a shard.

One of the largest dangers of this kind of a system is those targets getting overwritten on accident:

Say you have an avatar with a dynamic variable broadcasting a slot to User/WeldingMaskFace (User is a variable space automatically added to every user, the users equipped avatar and held items are under the space). If you are wearing one copy of the avatar, then pick up a second copy of the avatar in your hand, the same dynamic variable will exist in both the equipped avatar and the held avatar, and the value of the variable will collapse to one of those two values.

Even if the second avatar is dropped, shards that target the variable may attach to the wrong instance of the avatar, or not instance at all. 

To get around this creators should follow two rules: 
Always have the parent object contain the dynamic variable space. For avatars the common convention is to add a dynamic variable space of Avatar to the avatar root, and have the shard variables exist in that variable space.
For any values that do not need to change, drive the value so it can never change. This causes errors in the Resonite log if multiple drives happen to the same variable, but the variables should return to their expected state once the multi drive case resolves.
Instance Auto Destruction
There's a number of ways to destroy an object in Resonite, and many of them didn't respect auto cleanup callbacks.
Instance to Unit Transform
Instanced objects will by default be at the same world orientation and scale of the shard itself, having a shard set the instanced object to unit transform ( [0,0,0] position, [0,0,0] rotation, and [1,1,1] scale ) will avoid a lot of odd positioning issues.

Reposition the slot the instance is being positioned under to move there the instance is positioned.
