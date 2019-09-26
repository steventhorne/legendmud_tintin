# Table of Contents
- [Overview](#overview)
- [Installation](#installation)
    - [Linux](#linux)
    - [Windows](#windows)
- [Usage](#usage)
- [Config](#config)
- [Modules](#modules)
    - [Macros Module](#macros-module)
    - [Logging Module](#logging-module)
    - [Combat Module](#combat-module)
        - [Combat Aliases](#combat-aliases)
    - [Map Module](#map-module)
        - [Map Aliases](#map-aliases)
    - [Prompt Module](#prompt-module)
    - [Chat Module](#chat-module)
- [Custom Modules](#custom-modules)
- [Classes](#classes)
    - [Class Aliases](#class-aliases)
    - [Custom Classes](#custom-classes)

# Overview

This is an all-in-one package for TinTin++ to play LegendMUD.
A few of the features include:
- An autologin system
- A map with mapping triggers
- General purpose combat triggers and aliases
- A system for loading aliases and triggers by class name

This package also comes with triggers based on my specific prompt and channel formats.
This is an optional feature of the package, but some features will not work without updating my channel format triggers, and altering the prompt file or acquiring my prompt.
The following features will not work without loading the prompt file or updating the channel format triggers:
- A single prompt at the bottom of the screen (instead of repeating with every incoming message)
- Preventing splitting of gold when getting gold from your own corpse
- Including area name in new rooms added to the map
- Using the area name to help find the room you're in on the map
- Logging of channels and tells to chat.txt and displaying them with `./showchat`

# Installation
Install TinTin++ on your system.
This package requires you to use at least TinTin++ version 2.01.90.

## Linux
Clone this repository to a directory on your system.

## Windows
Navigate to %APPDATA%\WinTin++\bin and clone this repository to the bin directory.
The core.tin file should be in the root of the bin directory.

Navigate up to the WinTin++ directory, right click on the WinTin++ shortcut and click properties.
Change the `main.tin` at the end of the Target field to `core.tin`.

# Usage
To run TinTin++ with this package, simply run `tt++ core.tin` in the root of this directory.

# Config
After running `tt++ core.tin` for the first time, there will be two config files that you can modify:
- sys.config
- user.config

The `sys.config` config contains settings for the TinTin++ client.
The `user.config` config contains settings for this package.
You will need to restart the client for any changed settings to take effect.

You can add your own custom settings to these files if you need more for your scripts.

# Modules
This package comes with optional modules that can be enabled or disabled at your discretion.
Modules are TinTin++ scripts that are automatically loaded as soon as the client starts.
These are different from [Classes](#classes) which can be loaded and unloaded after the client has started.

In order to enable a module, exit TinTin++ and edit the user.config file.
Within this file you will find the following line:
`#VARIABLE         {modules}  {logging;combat;map}`

Add the module identifier to the list of modules in this variable.
For example, if you wanted to enable the prompt module:
`#VARIABLE         {modules}  {logging;combat;map;prompt}`

Next time you run TinTin++, the module will be enabled.

In order to reload a module after making changes to the module's file, use the `reload` alias.
For example: `reload all` will reload all modules, while `reload <module name>` will reload a specific module.

***Please note that some of these modules may require extra work in order to use.***

## Macros Module
> Identifier: macros | Default: enabled

The macros modules includes a few macros to make playing LegendMUD a little easier.

Feel free to disable this and create your own custom macros module.

## Logging Module
> Identifier: logging | Default: enabled

The logging module will log the text of the game to log files in the `logs` folder.
Each day a new log file will be created with that date as the filename.

## Combat Module
> Identifier: combat | Default: enabled

The combat module has some general purpose aliases and actions for use in combat. More specific aliases and actions may be found in classes.

### Combat Aliases
|Alias|Description|Usage|
|:----|:----------|:----|
|setrush|Sets the response for the rush trigger, %1 is the friendly and %2 is the enemy|`setrush resc %1`, `setrush rage %2`. `setrush #nop` will disable the trigger|

## Map Module
> Identifier: map | Default: enabled

The map module includes a pre-built map, automatic following, and mapping tools for the MUD.

Display the map with one of the following methods:
- Typing `#map map` will display the map on demand
- Update the following user.config settings
    - {map_vtmap} {on}
    - {split_top} {16}
- Navigate to map/ in a separate terminal and run `./showmap`

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

## Prompt Module
> Identifier: prompt | Default: disabled

The prompt module will capture the prompt and keep a single copy at the bottom of the screen.
This module will not work out of the box. You have two options:
- Update the `prompt.tin` module to work with your prompt
- Acquire my prompt

If you want to acquire my prompt, enter the game and type `prompt acquire Svartur`.
**Note that this will replace your prompt. Save a backup of your prompt code somewhere if you need it.**

## Chat Module
> Identifier: chat | Default: disabled

The chat module will capture all channel and tells and log them to a chat.txt file which can be displayed in a separate terminal or used for other purposes.

This module will not work out of the box. If you would like to use this module, update the `chat.tin` module to work with your channel messages.

# Custom Modules
You can create your own modules by creating a `.tin` file with your scripts.
Put the new `.tin` file in the `modules/` directory and add it to the user.config to have your new module automatically loaded.

This is great for creating your own custom content without altering the files in this package.

You can also use the `reload` alias to reload custom modules.
For example: `reload all` will reload all modules, while `reload <module name>` will reload a specific module.

# Classes
This package has support for loading character specific classes on the fly.

An example of this would be logging into a vina mage and loading up the vina class which would contain alaises for the associated spells.

## Class Aliases
|Alias|Description|Usage|
|:----|:----------|:----|
|loadclass|Loads a class file which can be unloaded later|`loadclass tank`, `loadclass vina`, `loadclass kere`|
|killclass|Unloads a class file that has been loaded via `loadclass`|`killclass tank`, `loadclass vina`, `loadclass kere`|

## Custom Classes
You can create your own classes by creating a `.tin` file with your scripts.
Put the new `.tin` file in the `classes/` directory and you can load it with the `loadclass` alias without restarting TinTin++.
