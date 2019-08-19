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

Rename the "config_example" file to "config". Replace the `<bracket text>` with your information.

Display the map with one of the following methods:
- Typing `#map map` will display the map on demand
- Set `#map flag vtmap on` and set `#split 16 1` if not using my prompt file, or update the prompt.tin file to say `#SPLIT 16 3` instead of `#SLPIT 0 3`
- Navigate to map/ in a separate terminal and run `./showmap`

To acquire my prompt simply enter the game and type `prompt acquire Svartur`.
**Note that this will replace your prompt. Save a backup of your prompt code somewhere if you need it.**

# Usage
There are some aliases that can be viewed by typing `#ALIAS`.

These include:
- enmap - enable edit mode for the map
- dismap - disable edit mode for the map
- door - adds a door in the map (ex: `door e`, `door n`, `door w`, etc.)
- rname - gives a room a nickname on the map (ex: `rname jb`, `rname stag`)
- search - finds a room based on its nickname and jumps to it (ex: `search jb`, `search stag`)
- find - finds a room based on your current room name and description and jumps to it (ex: `find`)
- walk - finds a room based on its nickname and walks you to it (ex: `walk jb`, `walk stag`)
- savemap - saves the map to file
- loadclass - loads a class file which will allow you to unload it later (ex: `loadclass tank`)
- killclass - unloads a class that has been loaded via `loadclass` (ex: `killclass tank`)
