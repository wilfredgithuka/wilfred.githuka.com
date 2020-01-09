---
title:       "How to Enable Nerdy Stats in Euro Truck Simulator"
subtitle:    "The technical stats and render info are available for devs to explore"
description: "Euro Truck Simulator 2 is a high rated truck simulator game available for Linux users under steam." 
date:        "2019-01-19"
author:      "Wilfred Githuka"
image:       "/img/city_view.png"
tags:        ["ets", "gaming"]
categories:  ["ETS2" ]
---

The developer console is not just a powerful tool to gain immediate access to certain game variables and commands for power users, mappers, modders and so on.
It's also something your average user might want to have enabled for reporting bugs, taking screenshots (though the new photo edit mode is good for that as well) and for mod users who want to see if that new mod he installed has any issues. Errors will be shown in red in the console so you don't have to check your game log to know if the mod worked or not.

These settings are similar to both ETS and ATS

## Enable Developer Mode

To enable the dev mode, open the file config.cfg. This is located in `~/.local/share/Euro\ Truck\ Simulator\ 2/`

Change the following values from 0 to 1 as follows:

* uset g_developer "1" 
* uset g_console "1"

Save the file.

You are now in developer mode :-)

## Enable Nerdy Stats

Start the game, the following settings shall be made during game-play

Press the Tilde key (key above Tab) to show the commands available. The tab key can help you with autocompleting. 

Please note that any changes you make here will cause the game to change abit and sometimes you may not realise, 
so be careful what you change here since there are many commands listed here.

After pressing the Tilde key, enter `g_minicon 1` to set the mini console to 1 then enter to show the nerdy stats. You can set it to 0 
to turn them off if you dont fancy them there.

During th gameplay you dont have to worry about the yellow stats shown. Anything in red is what is supposed to worry you.

![image1](/img/neat.png)

You can expore other commands listed there and see what they do.
