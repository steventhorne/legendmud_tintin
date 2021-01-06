# Table of Contents
- [Overview](#overview)
- [Installation](#installation)
    - [Linux](#install-linux)
    - [macOS](#install-mac)
    - [Windows](#install-windows)
- [Usage](#usage)
    - [Linux and macOS](#usage-linux)
    - [Windows](#usage-windows)
- [Config](#config)
- [Layouts](#layouts)
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
- [Help Files](#help-files)
- [FAQ](#faq)

# Overview

![Version v=19.10.0](http://img.shields.io/badge/version-v=2.1.0-brightgreen.svg?style=flat-square) [![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

This is an all-in-one package for TinTin++ to play LegendMUD.
A few of the features include:
- An autologin system
- A map with mapping triggers
- General purpose combat triggers and aliases
- A system for loading aliases and triggers by class name
- Built in layout selection and customization

This package also comes with triggers based on my specific prompt.
This is an optional feature of the package and will not work without acquiring my prompt format.
The following features will not work without acquiring my prompt format:
- A single prompt at the bottom of the screen (instead of repeating with every incoming message)
- Preventing splitting of gold when getting gold from your own corpse
- Using the area name to help find the room you're in on the map

# Installation
[Download](https://tintin.sourceforge.io/download.php) and install TinTin++ on your system.
This package requires you to use at least TinTin++ version 2.02.01.

[Download](https://github.com/steventhorne/legendmud_tintin/releases/latest) the latest release of this package.
Do not download the repository as it may not be a stable release.

## Linux {#install-linux}
Download the latest release to a directory on your system.

## macOS {#install-mac}
If you have [Homebrew](https://brew.sh) installed, from Terminal run
```
brew install tintin
```

## Windows {#install-windows}
Navigate to %APPDATA%\WinTin++\bin and download the latest release to the bin directory.
The core.tin file should be in the root of the bin directory.

Navigate up to the WinTin++ directory, right click on the WinTin++ shortcut and click properties.
Change the `main.tin` at the end of the Target field to `core.tin`.

# Usage
## Linux and macOS {#usage-linux}
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
You will need to restart the client or type `reloadmodule` for any changed settings to take effect.

You can add your own custom settings to these files if you need more for your scripts.

# Layouts
This package comes with built-in layouts that allow you to display additional information outside of the main MUD output.
In order to see the layouts that are available to you, you can type the alias `layouts` in game.

The `layouts` alias will output the following:
```
1              2              3              4
 ___________    ___________    ___________    ___________
|           |  |           |  |     |     |  |           |
|           |  |     1     |  |     |     |  |     1     |
|     M     |  |___________|  |  M  |  1  |  |___________|
|           |  |           |  |     |     |  |     |     |
|           |  |     M     |  |     |     |  |  M  |  2  |
|_____ _____|  |___________|  |_____|_____|  |_____|_____|
5              6              7              8
 ___________    ___________    ___________    ___________
|     |     |  |     |     |  |     |     |  |     |     |
|  1  |     |  |  1  |  2  |  |     |  1  |  |  1  |  2  |
|_____|  2  |  |_____|_____|  |  M  |_____|  |_____|_____|
|     |     |  |           |  |     |     |  |     |     |
|  M  |     |  |     M     |  |     |  2  |  |  M  |  3  |
|_____|_____|  |___________|  |_____|_____|  |_____|_____|
```

You can choose a layout by setting the layout configuration in the user.config file to one of the layout numbers above.

After choosing a layout, you can specify which pane each module will display in using the {pane_<module name>} configurations in the user.config file.

Layouts other than the the first layout may use the {height_percent} and {width_percent} user.config settings. These percentages decide what percentage of the screen the main(M) pane takes up. These are defaulted to 60%.

**NOTE: Currently only the map and chat modules have display panes, but this may change in the future.**

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

Next time you type `reloadmodule` or restart TinTin++, the module will be enabled.

## Module Aliases
|Alias|Description|Usage|
|:---|:---|:---|
|reloadmodule|Reloads the entire package including config files.|`reloadmodule`|
|reloadmodule <module name>|Reloads a specific module in case changes have been made to the file.|`reloadmodule map`, `reloadmodule prompt`, `reloadmodule all`|

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

The combat module includes an auto-flee trigger that will automatically send additional flee attempts if you fail a flee. To disable this, update the `auto_flee` option in `user.config`.

### Combat Aliases
|Alias|Description|Usage|
|:----|:----------|:----|
|setrush|Sets the response for the rush trigger, %1 is the the enemy and %2 is the friendly|`setrush resc %2`, `setrush rage %1`. `setrush #nop` will disable the trigger|

## Map Module
> Identifier: map | Default: enabled

The map module includes a pre-built map, automatic following, and mapping tools for the MUD.
**Note:** The map is stored in a single file. If you decide to edit your copy of the map, any updates to the map in this repo will need to overwrite your changes.

Display the map with one of the following methods:
- Typing `#map map` will display the map on demand
- Use a layout other than the first layout and set the {pane_map} setting in the user.config to a valid pane number.
    - the {map_vtmap} and {split_top} settings are no longer necessary or used.
- Set `map_external*` settings in `user.config`. Navigate to map/ in a separate terminal and run `./showmap`

### Map Aliases
|Alias|Description|Usage|
|:----|:----------|:----|
|enmap|Enable edit mode for the mapper|`enmap`|
|dismap|Disable edit mode for the mapper|`dismap`|
|door|Adds a door to the specified exit|`door e`, `door n`, `door w`, etc.|
|rname|Gives a room a nickname in the map|`rname jb`, `rname stag`|
|search|Searches for rooms in the map with the specified text in the room name.|`search Harbor`, `search Royal Stag`|
|find|Finds a room based on your current room in the MUD and teleports to it|`find`|
|run|Finds a room based on the specified nickname and runs you to it if a path is found|`run jb`, `run stag`|
|walk|Finds a room based on the specified nickname and walks you to it if a path is found|`walk jb`, `walk stag`|
|slowwalk|Finds a room based on the specified nickname and walks **slowly** to it if a path is found|`slowwalk jb`, `slowwalk stag`|
|stop|Stops a `slowwalk` command.|`stop`|
|nicknames|Lists all rooms that have nicknames|`nicknames`|
|savemap|Saves the map to file|`savemap`|

*Note: the difference between `run` and `walk` is the speed of the map update. `Run` will update the map to the destination instantly, while `walk` will do it more slowly.*

## Prompt Module
> Identifier: prompt | Default: disabled

The prompt module creates a complex prompt and keeps a single copy at the bottom of the screen.
This module will work out of the box, but will **not** take your prompt into account.
You can have your own in-game prompt in addition to this prompt, or use the in-game `prompt` command to disable your in-game prompt and only use this prompt.

In the future, this module may support custom prompts.

## Chat Module
> Identifier: chat | Default: disabled

The chat module will capture all channel and tells and log them to a chat.txt file which can be displayed in a separate terminal or used for other purposes.

Additionally, the chat module can be displayed in a separate pane.
This can be done by selecting a layout other than the first layout and setting the {pane_chat} setting in the user.config to a valid pane number.

The chat log can be scrolled through using the ALT+PGUP, ALT+PGDN, ALT+HOME, and ALT+END key combinations.

**Note**: This module may not work if you have changed your channel formats.

# Custom Modules
You can create your own modules by creating a `.tin` file with your scripts.
Put the new `.tin` file in the `modules/` directory and add the name to the user.config to have your new module automatically loaded.

This is great for creating your own custom content without altering the files in this package.

You can also use the `reloadmodule` alias to reload custom modules.

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

## Help Files
There are help files for each module that can be found by entering the `phelp` (short for package help) alias. Further help can be found by entering `phelp <alias name>`.

# FAQ
The TinTin++ FAQ can be found [here](https://tintin.sourceforge.io/faq.php)

## Why can't I select text to copy it?
This is because of the mouse tracking setting that's enabled for certain features that require mouse support.
You can select text by holding Shift.

## Why isn't the map following correctly?
This could be for any number of reasons.

If the map doesn't follow you when you input basic movement commands, make sure you're typing 'n, s, e, w, u, d' to move directions. These must be single characters and lowercase.

If the map doesn't locate you when you recall or use the 'find' command, make sure you are either using the prompt module, or have added the @$ prompt code to the end of your prompt format.

If the map doesn't follow you when you are following another character, you will need to disable moods via the 'mood seemoods' command. 

## How do I script X in TinTin++?
TinTin++ has a really complex and comprehensive scripting engine. While this can be daunting, there is a GREAT online manual available.

TinTin++ has support for two different syntaxes for capturing text.
There's standard PCRE Regex, and a custom Regex-lite that is specific to tt++.

I personally prefer the standard PCRE Regex, because there are a lot of resources online for it, including online regex testers. If you want to use the PCRE Regex you have to create your actions with double {{}}s.
Example:
`#action {{^Svartur bonks ([\w\=\'\.]+) on the head!$}} {{#send comf %2;}}`
I also use [Regex101](https://www.regex101.com) to test my regex patterns.

If you want to use the easy version, you use the single {}s.
Example:
`#action {^Svartur bonks %1 on the head!$} {#send comf %1;}}`

As you can see, the second variety **is** much easier to figure out, **BUT** it's also not able to accomplish as much as PCRE Regex. It also has no online testing tools.
