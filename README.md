# Overview

This package comes with a few things:
- A map with mapping triggers
- Core triggers and aliases
- A system for loading aliases and triggers by class name
- An autologin system

This package also comes with triggers based on my specific prompt and channel formats.
This is an optional feature of the package, but some features will not work without updating my channel format triggers, and altering the prompt file or acquiring my prompt.
The following features will not work without loading the prompt file or updating the channel format triggers:
- A single prompt at the bottom of the screen (instead of repeating with every incoming message)
- Preventing splitting of gold when getting gold from your own corpse
- Including area name in new rooms added to the map
- Using the area name to help find the room you're in on the map
- Logging of channels and tells to chat.txt and displaying them with `./showchat`

# Installation
Install Tintin++ on your system.
Download this repository to a directory on your system.

Rename the "config_example" file to "config". Replace the `<bracket text>` with your information.

If you want to acquire my prompt, enter the game and type `prompt acquire Svartur`.
**Note that this will replace your prompt. Save a backup of your prompt code somewhere if you need it.**

# Usage
To run Tintin++ with this package, simply run `tt++ core.tin` in the root of this directory.

## Aliases
There are some aliases that can be viewed by typing `#ALIAS`.

### Map Aliases
|Alias|Description|Usage|
|:----|:----------|:----|
|enmap|Enable edit mode for the mapper|`enmap`|
|dismap|Disable edit mode for the mapper|`dismap`|
|door|Adds a door to the specified exit|`door e`, `door n`, `door w`, etc.|
|rname|Gives a room a nickname in the map|`rname jb`, `rname stag`|
|search|Finds a room based on the specified nickname and teleports to it|`search jb`, `search stag`|
|find|Finds a room based on your current room in the MUD and teleports to it|`find`|
|walk|Finds a room based on the specified nickname and walks you to it if a path is found|`walk jb`, `walk stag`|
|nicknames|Lists all rooms that have nicknames|`nicknames`|
|savemap|Saves the map to file|`savemap`|

### Other Aliases
|Alias|Description|Usage|
|:----|:----------|:----|
|loadclass|Loads a class file which can be unloaded later|`loadclass tank`|
|killclass|Unloads a class file that has been loaded via `loadclass`|`killclass tank`|

## Map
Display the map with one of the following methods:
- Typing `#map map` will display the map on demand
- Set `#map flag vtmap on` and set `#split 16 1` if not using my prompt file, or update the prompt.tin file to say `#SPLIT 16 3` instead of `#SLPIT 0 3`
- Navigate to map/ in a separate terminal and run `./showmap`
