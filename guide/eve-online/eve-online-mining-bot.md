# EVE Online Mining Bot

For this guide, I picked a mining bot optimal for beginners, which means easy to set up and use. After several iterations in development, this bot has matured to be robust regarding interruptions and changes in the game environment.

Maybe you have seen some bots or 'macros' which follow a fixed sequence of actions to perform an in-game task. The bot we will use here does not just follow a rigid series of steps but frequently looks at the current state of the game to decide the next action. This also means it can detect if it failed to perform a particular subtask, (for example, warping to the mining site) and try again. So it also does not matter if your ship is docked or in space when you start the bot.

Before going into the setup, a quick overview of this bot and what it does:

+ When the mining hold is not full, warps to an asteroid belt.
+ Uses drones to defend against rats if available.
+ Mines from asteroids.
+ When the mining hold is full, warps and docks to a station or structure to unload the ore into the item hangar. (It remembers the station in which it was last docked, and docks again at the same station.)
+ Runs away if shield hitpoints drop too low (The default threshold is 70%).
+ Displays statistics such as the total volume of unloaded ore, so that you can easily track performance.
+ Closes message boxes that could pop up sometimes during gameplay.

## Setting up the Game Client

Despite being quite robust, this mining bot is far from being as smart as a human. For example, its perception is more limited than ours, so we need to set up the game to make sure that the bot can see everything it needs to. Following is the list of setup instructions for the EVE Online client:

+ Set the UI language to English.
+ In the ship UI in the 'Options' menu, tick the checkbox for 'Display Module Tooltips'.
+ In Overview window, make asteroids visible.
+ Set the Overview window to sort objects in space by distance with the nearest entry at the top.
+ Open one inventory window.
+ If you want to use drones for defense against rats, place them in the drone bay, and open the 'Drones' window.

## Starting the Mining Bot

If the BotLab client is not already installed on your machine, follow the guide at <https://to.botlab.org/guide/how-to-install-the-botlab-client>
The BotLab client is a tool for developing bots and also makes running bots easier with graphical user interfaces for configuration.

In the BotLab client, load the bot by entering the following link in the 'Select Bot' view:
<https://catalog.botlab.org/ed9b5acc9cebd2c4>

There is a detailed walkthrough video on how to load and run a bot at <https://to.botlab.org/guide/video/how-to-run-a-bot-live>

The bot needs a few seconds to start and find the EVE Online client process. It also shows status messages to inform what it is doing at the moment and when the startup is complete.

![EVE Online Bot Starting](./image/2023-03-08-botlab-gui-eve-online-bot-startup.png)

From here on, the bot works automatically. It detects the topmost game client window and starts working in that game client.

In case the bot does not work as expected, the first place to look is in the status message of the bot. Depending on what the bot is seeing and doing at the moment, it can display many different status messages.
For example, if you disable the location ('System info') info panel in the EVE Online client, the bot displays the following message:

> I cannot see the location info panel.

As soon as you enable this info panel again, the bot will also continue working.

The bot repeats the cycle of mining and unloading until you tell it to pause (`SHIFT` + `CTRL` + `ALT` keys) or stop it.

To give an overview of the performance of the bot, it displays statistics like this:

> Session performance: times unloaded: 13, volume unloaded / m³: 351706

## Configuration Settings

All settings are optional; you only need them in case the defaults don't fit your use-case.

+ `mining-site` : Name of a mining location, as it appears in the 'Label' column of the 'Locations' window.
+ `unload-station-name` : Name of a station to dock to when the mining hold is full.
+ `unload-structure-name` : Name of a structure to dock to when the mining hold is full.
+ `activate-module-always` : Text found in tooltips of ship modules that should always be active. For example: "shield hardener".
+ `hide-when-neutral-in-local` : Should we hide when a neutral or hostile pilot appears in the local chat? The only supported values are `no` and `yes`.
+ `unload-fleet-hangar-percent` : This will make the bot unload the mining hold at least XX percent full to the fleet hangar, you must be in a fleet with an orca or a rorqual and the fleet hangar must be visible within the inventory window.
+ `dock-when-without-drones` : This will make the bot dock when it's out of drones. The only supported values are `no` and `yes`.
+ `repair-before-undocking` : Repair the ship at the station before undocking. The only supported values are `no` and `yes`.
+ `afterburner-module-text` : Text found in tooltips of the afterburner module.
+ `afterburner-distance-threshold` : Distance threshold (in meters) at which to activate/deactivate the afterburner.

When using more than one setting, start a new line for each setting in the text input field.
Here is an example of a complete settings string:

```
mining-site = mining bookmark label
unload-station-name = Noghere VII - Moon 15
activate-module-always = shield hardener
activate-module-always = afterburner
```

The bot searches the configured structure or station name in the 'Locations' window and all overview windows.
If the destination is not visible in the locations and overview windows, it opens the 'surroundings' menu to search for it.
When using the 'Locations' window, enter the unload station/structure name as it appears in the 'Label' column.


## Running Multiple Instances

This bot supports running multiple instances on the same desktop. In such a scenario, the individual bot instances take turns sending input and coordinate to avoid interfering with each other's input. To learn more about multi-instance setup, see <https://to.botlab.org/guide/running-bots-on-multiple-game-clients>

----

If you want to learn how this bot or other apps for EVE Online are developed, have a look at the directory of development guides at <https://to.botlab.org/guide/overview>

In case I forgot to add something here or you have any questions, don't hesitate to ask on the [BotLab forum](https://forum.botlab.org/).
