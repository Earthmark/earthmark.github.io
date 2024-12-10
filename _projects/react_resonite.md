---
title: React-Resonite
excerpt: Supporting React.js for instancing, updating, and printing resonite objects. 
---

Supporting React.js for instancing, updating, and printing resonite objects. 

**Status:** Tabled due to: in-Resonite performance issues consuming update messages, updates to the current react version are needed.
{: .notice}

A node.js library and Resonite object that proxied commands between a react virtual DOM and a pseudo Resonite DOM.

Or put another way, write jsx code and it makes Resonite objects.

The library had two parts, an in Resonite library, and a JavaScript descriptor library. 

In Resonite the dev creates prefab objects that represent a DOM node, using a special slot to wrap bindings that are exposed in js. These nodes can be as complex as the dev wants, it could be as high order as each node being a ship in an ocean, and each ship being many thousands of slots, where a value exposed to js is adapted heavily before being used in the world. 

From there the dev creates a descriptor object in JavaScript that creates update logic, and provides intellisense support.

From there the dev creates jsx component trees just as they would for html, instead using the primitives they defined in the descriptor object.

Once a Resonite client connects via a websocket, an instance of the react DOM is created and messages are passed back and forth between the two environments. 

It is possible to use this to share state between multiple Resonite sessions, as a single node server can run any number of sessions.

# What Killed the Project

One use case for this project was a precursor for the inventory viewer, where every link and node was an object inside of Resonite and you could view the same content via a Resonite world. 

The viewer would create an object for every node and link between nodes. 

Each object contained at least 5 dynamic variables, only some of which were used, but all were defined on every object.

Spawning a slot requires at least two commands, one to create the object, and a second that is fired two update frames later once the dynamic variables hook up as their names update.

At the time, Resonite could handle about 60 messages per update frame before the updating user lags extremely noticeably, around 240 messages per second at 40 fps.
The nodejs side could produce hundreds of thousands of messages in under a second.

The nodejs side of the viewer would run, send the messages over, and Resonite would chug for minutes trying to process the messages.

During that time dynamic variables were being renamed, added, and instanced. It turns out moving a variable (or renaming one) takes an amount of time relative to all variables in the space. As the create messages were processed, the world would get slower and slower until every user was at single digits (renaming affected every user).

Once all messages were processed, Resonite ran at full fps. If you reparented any part of the tree above the object though, everyone in the session would hang for a few seconds.

This is what led to the idea of printer mode where you could instance an object, then automatically strip out the dynamic variables.
