---
title: Inventory Viewer
excerpt: A way to view the used storage of a Resonite account so users could more easily free storage if they ran out.
---

A way to view the used storage of a Resonite account so users could more easily free storage if they ran out.

**Status:** Alpha version available, looking for more maintainers
{: .notice}

Removing storage gets complicated for two big reasons: 
Items that share assets, only count once.
If you remove 20 copies of an avatar, you may remove very little storage if there is a 21st copy that stores the same 4k textures and chunky model. 
Some assets are free
The homeworld and everything inside of it is always free and never counts against your storage.

Additionally voice messages also count against your storage, but the only way to delete them is to send a message to the Resonite bot directly. 

The visualizer reads the manifest file that lists all records in an account, and groups records by how much storage they share between assets. From there you can filter and see how you can strategically see what records you could delete to get back within storage bounds.
