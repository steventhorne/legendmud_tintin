# Table of Contents
- [Overview](#overview)
- [Installation](#installation)
    - [Linux](#install-linux)
    - [Windows](#install-windows)
- [Usage](#usage)
    - [Linux](#usage-linux)
    - [Windows](#usage-windows)
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
- [FAQ](#faq)

# Overview

![Version v=19.10.0](http://img.shields.io/badge/version-v=2.1.0-brightgreen.svg?style=flat-square) [![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

This is an all-in-one package for TinTin++ to play LegendMUD.
A few of the features include:
- Automatic updates
- An autologin system
- A map with mapping triggers
- General purpose combat triggers and aliases
- A system for loading aliases and triggers by class name

This package also comes with triggers based on my specific prompt.
This is an optional feature of the package and will not work without acquiring my prompt format.
The following features will not work without acquiring my prompt format:
- A single prompt at the bottom of the screen (instead of repeating with every incoming message)
- Preventing splitting of gold when getting gold from your own corpse
- Using the area name to help find the room you're in on the map

# Installation
[Download](https://tintin.sourceforge.io/download.php) and install TinTin++ on your system.
This package requires you to use at least TinTin++ version 2.01.90.

[Download](https://github.com/steventhorne/legendmud_tintin/releases/latest) the latest release of this package.
Do not download the repository as it may not be a stable release.

## Linux {#install-linux}
Download the latest release to a directory on your system.

## Windows {#install-windows}
Navigate to %APPDATA%\WinTin++\bin and download the latest release to the bin directory.
The core.tin file should be in the root of the bin directory.

Navigate up to the WinTin++ directory, right click on the WinTin++ shortcut and click properties.
Change the `main.tin` at the end of the Target field to `core.tin`.

# Usage
## Linux {#usage-linux}
To run TinTin++ with this package, simply run `tt++ core.tin` in the root of this directory.

## Windows {#usage-windows}
Run the WinTin++ shortcut.

# Config
After running Tintin++ with this package for the first time, there will be two config files that you can modify:
- sys.config
- user.config

The `sys.config` config contains settings for the TinTin++ client.
You will need to restart the client for any changed settings to take effect.

The `user.config` config contains settings for this package.
You will need to restart the client or type `reload` for any changed settings to take effect.

You can add your own custom settings to these files if you need more for your scripts.

# Modules
This package comes with optional modules that can be enabled or disabled at your discretion.
Modules are TinTin++ scripts that are automatically loaded as soon as the client starts and will run regardless of the character your logged in as.
These are different from [Classes](#classes) which can be loaded and unloaded after the client has started.

In order to enable a module, edit the user.config file.
Within this file you will find the following line:
`#VARIABLE         {modules}  {logging;combat;map}`

Add the module identifier to the list of modules in this variable.
For example, if you wanted to enable the prompt module:
`#VARIABLE         {modules}  {logging;combat;map;prompt}`

Next time you type `reload` or restart TinTin++, the module will be enabled.

## Module Aliases
|Alias|Description|Usage|
|:---|:---|:---|
|reload|Reloads the entire package including config files.|`reload`|
|reload <module name>|Reloads a specific module in case changes have been made to the file.|`reload map`, `reload prompt`, `reload all`|

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
**Note:** The map is stored in a single file. If you decide to edit your copy of the map, any updates to the map in this repo will need to overwrite your changes.

Display the map with one of the following methods:
- Typing `#map map` will display the map on demand
- Update the following user.config settings
    - {map_vtmap} {on}
    - {split_top} {16} (this can be any number in order to change the size)
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
|slowwalk|Finds a room based on the specified nickname and walks **slowly** to it if a path is found|`slowwalk jb`, `slowwalk stag`|
|stop|Stops a `slowwalk` command.|`stop`|
|nicknames|Lists all rooms that have nicknames|`nicknames`|
|savemap|Saves the map to file|`savemap`|

## Prompt Module
> Identifier: prompt | Default: disabled

The prompt module will capture the prompt and keep a single copy at the bottom of the screen.
This module will not work out of the box. You will need to acquire my prompt in order to use it.

If you want to acquire my prompt, enter the game and type `prompt acquire Svartur`.
**Note**: this will replace your prompt. Save a backup of your prompt code somewhere if you need it.

## Chat Module
> Identifier: chat | Default: disabled

The chat module will capture all channel and tells and log them to a chat.txt file which can be displayed in a separate terminal or used for other purposes.

**Note**: This module may not work if you have changed your channel formats.

# Custom Modules
You can create your own modules by creating a `.tin` file with your scripts.
Put the new `.tin` file in the `modules/` directory and add the name to the user.config to have your new module automatically loaded.

This is great for creating your own custom content without altering the files in this package.

You can also use the `reload` alias to reload custom modules.

# Classes
Classes are TinTin++ scripts that can be loaded on the fly for specific situations and then unloaded when they're no longer needed.
These are different from [Modules](#modules) which are loaded as soon as the client starts and stay loaded for the duration of the session.

An example of this would be logging into a vina mage and loading the vina class which would contain alaises for the associated spells.

## Class Aliases
|Alias|Description|Usage|
|:----|:----------|:----|
|loadclass|Loads a class file which can be unloaded later|`loadclass tank`, `loadclass vina`, `loadclass kere`|
|reloadclass|Reloads a class if changes have been made to the file.|`reloadclass tank`, `reloadclass vina`, `reloadclass kere`, `reloadclass all`|
|killclass|Unloads a class file that has been loaded via `loadclass`|`killclass tank`, `killclass vina`, `killclass kere`, `killclass all`|

## Custom Classes
You can create your own classes by creating a `.tin` file with your scripts.
Put the new `.tin` file in the `classes/` directory and then load it with the `loadclass` alias without restarting TinTin++.

# FAQ
The TinTin++ FAQ can be found [here](https://tintin.sourceforge.io/faq.php)

## Why can't I select text to copy it?
This is because of the mouse tracking setting that's enabled for certain features that require mouse support.
You can select text by holding Shift.
