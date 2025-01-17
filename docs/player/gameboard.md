# Game Board

This is PlanarAlly's heart.
When playing, you will mostly interact with the game board, moving tokens over a map that shows (or does not show) your character's surroundings and other PC and NPC characters around them.

:::warning The big red border
Most actions you perform have to be synchronized with the server.
In case this connection is lost for whatever reason, a thick red border around the screen will warn you.
Any changes you made during a disconnect might be lost.
:::

## Overview

This document gives a brief technical introduction to the concepts of locations, floors and layers.
This is not required reading for a player, but might give more insights into the behaviour of certain systems.
As a DM there is more in-depth info for each of these concepts under the DM section.

PlanarAlly organizes campaigns using 3 concepts. A campaign has 1 or more **locations**, which each consist of 1 or more **floors**, which each consist of a fixed set of **layers**.
All of these together culminate in a scenario that is being drawn on the screen with which you interact.

As a player you are usually not able to change the active location, floor or layer,
but you nonetheless still interact with these concepts everytime you move a shape.

<!-- The board consists of several _layers_ that are drawn on top of each other.
PlanarAlly calls a complete set of these layers a _floor_.
Floors can be stacked vertically atop of each other.
A set of floors is called a _location_.
Locations are, if you want, sets of floors that are stacked horizontally.

As a player, you won't be able to see all layers and you won't be able to interact with all layers you see.
Also, you might not be able to see all floors and you might not be able to enter floors you can see.
You will also only _see_ one location at a time.

The layers are introduced below with the functionality relevant for players.
They are documented in-depth with also DM-only functionaltiy [within an own page in the DM-section of this documentation](/docs/dm/layers/). -->

## Locations

At the very top of organization is the concept of locations.
A campaign has at least 1 but can have multiple locations.

A location can be thought of as a specific instance of your game world.
It can be a very specific building the party is exploring or a higher level view of a village or maybe even the world map.

A player is at any moment in time always interacting with exactly 1 location, but the DM can move the players around as they move through the world.

See the [DM documentation on locations](/docs/dm/locations/) for more information.

## Layers

When you are loading a location, things have to be drawn on your screen.
You expect to see a map, your character tokens and maybe some light or shadow.

Although all these things seem to be on the same 2D plane, PlanarAlly actually stacks a couple of **layers** on top of eachother.

As a player you can only interact with the _tokens_ layer.
This is the main layer where you move your tokens and shapes you've drawn.

There are some other layers a player can see, but not interact with: the map layer and grid layer being the most obvious examples.
These both are rendered below the tokens layer.

Some other layers are completely invisible to players.
The DM layer for example is only visible to the DM and can be used to hide secrets until they become relevant.

For more in-depth explanation of the different layers, check the [DM docs](/docs/dm/layers/)!

## Floors

With just locations and layers we are set to play games.
PlanarAlly however has one extra trick up its sleeve.

A collection of layers is called a **floor**.
A location always has 1 but could be extended to have multiple floors.

When discovering a spooky mansion you are bound to move up or down some stairs.
When you move up a stairwell you ideally don't want the DM to have too much work to move your token to the map for that floor.
Maybe a different PA location could be used or another area in the active location, but this is just clunky.

PA floors are a tool that offer the DM to organize these sort of things more fluently.
Just like a real building the PA floors are rendered on top of eachother, and thus you might be able to see the floors below the floor you are present on.

A common example for this would be a window, balcony, or even a hole in the boarding.
So if there is nothing hindering your sight, you can still see some things happening on the floors below (e.g. when looking out of a window).

If the DM allows you to change floors manually, you can access them in the menu at the bottom left of your screen or use one of the keybindings.
Note that you might not be able to see everything on a different floor, depending on the [lighting](/docs/dm/light-shadows) and whether you have sufficient access to the tokens on this floor.
