A guide on how to **download** and **install mods** in [ARK: Survival Ascended](https://store.steampowered.com/app/2399830/ARK_Survival_Ascended/) on PC and on consoles.

ARK: Survival Ascended does modding differently from most games, and differently from ARK: Survival Evolved before it. There is no Steam Workshop here. All ASA mods live on [CurseForge](https://www.curseforge.com/ark-survival-ascended), the game has a mod browser built into it, and mods work on **PlayStation 5 and Xbox Series X|S as well as PC**. Cross-platform modding is a headline feature rather than a footnote.

That also means the answer to "how do I install a mod" is shorter than you might expect. Our example is [Better Horde Mode](https://www.curseforge.com/ark-survival-ascended/mods/better-horde-mode-qol-open-source), a quality of life mod for the game's horde events.

[**View Guide On TMC (Recommended Due To Better Formatting)**](https://moddingcommunity.com/blog/how-to-install-mods-in-ark-survival-ascended/)

## Table Of Contents
* [Requirements](#requirements)
* [How ASA Modding Works](#how-asa-modding-works)
    * [No Steam Workshop](#no-steam-workshop)
    * [Mod Project IDs](#mod-project-ids)
* [Installing Mods In Single Player](#installing-mods-in-single-player)
* [Joining A Modded Server](#joining-a-modded-server)
* [Consoles](#consoles)
* [Adding Mods To Your Own Server](#adding-mods-to-your-own-server)
* [The TMC App](#the-tmc-app)
* [Mod Load Order](#mod-load-order)
* [Configuring Mods](#configuring-mods)
* [Updating And Removing Mods](#updating-and-removing-mods)
* [Troubleshooting](#troubleshooting)
* [Conclusion](#conclusion)
* [See Also](#see-also)

## Requirements
* **ARK: Survival Ascended** on PC, PlayStation 5 or Xbox Series X|S.
* On PC: **Windows 10** or later. Linux players can run ASA through Proton, but there is no native Linux client.
* **A lot** of free space. A base ASA install is already large and mods are not small. Big overhaul mods and custom maps run into several GB each.
* Patience with download times. Mods come down through CurseForge's CDN rather than through Steam.

**NOTE** - ARK: Survival Evolved, the older game, uses Steam Workshop instead and works nothing like this. If you are on ASE, none of the steps below apply.

## How ASA Modding Works
### No Steam Workshop
Wildcard moved ASA modding to CurseForge so that mods could work on consoles, which Steam Workshop cannot do. The upshot is that mod installation is handled by the game itself rather than by Steam or by a mod manager on your PC.

There is no folder to copy `.pak` files into, no mod loader to install, and no load order file to hand-edit in the usual sense. The game downloads mods through its own integration and puts them where they belong.

This is genuinely simpler than most games in these guides. It also means you have less control when something goes wrong.

### Mod Project IDs
Every CurseForge mod has a numeric **Project ID**, and this is the identifier that actually matters. Server owners reference mods by ID, and it is the thing to quote when asking for help.

You will find it on the right-hand side of the mod's CurseForge page under **Details**. Better Horde Mode, for example, is Project ID `1163881`.

**TIP** - Keep a note of the Project IDs for your mod list. It is far more reliable than mod names, which change and which several mods often share.

## Installing Mods In Single Player
1. Launch ARK: Survival Ascended.
2. From the main menu, open the **Mods** section.
3. Browse or search the CurseForge catalogue from inside the game. Search for **Better Horde Mode**.
4. Select the mod and install it. The game downloads and installs it directly.
5. Once installed, enable the mod and start or load a single player world.

That is the whole process on PC and console alike. You never leave the game.

You can also browse on the [CurseForge website](https://www.curseforge.com/ark-survival-ascended) first, which is a much nicer way to read descriptions, screenshots and comments, then search for the mod by name in-game when you know what you want.

**WARNING** - Adding a content mod to an existing single player save is usually fine. Removing one is not. Mods that add creatures, items or structures leave data in the save that the game can no longer interpret, and the usual result is missing items or a broken world. Back up your saves before you experiment.

## Joining A Modded Server
This is where ASA's system is at its best. You do not install anything in advance.

1. Find the server in the in-game server browser and join it.
2. The game works out which mods the server is running and downloads them automatically.
3. Once they are down, you connect.

The first join to a heavily modded server can take a long while, because you may be pulling several GB. Subsequent joins are quick, since the mods are already local and only updates are fetched.

If you have already installed a mod by hand for single player and the server runs a different version, the game will update it as part of joining. It does not keep two copies.

## Consoles
Mods on PS5 and Xbox Series X|S work the same way as on PC. Open the **Mods** menu, browse CurseForge, install, and play. Joining a modded server downloads its mods automatically, exactly as it does on PC.

Two things to keep in mind:

* **Storage.** Consoles have less of it and ASA plus mods eats a lot. Keep an eye on free space.
* **Not every mod supports consoles.** Mods that rely on PC-only features are marked accordingly on CurseForge. The in-game browser on a console only shows you what will actually work there, which saves some frustration.

There is no PS4 or Xbox One version of ASA, so the older consoles are not part of this at all.

## Adding Mods To Your Own Server
If you run a dedicated server, mods are set on the command line with `-mods=`, using Project IDs rather than names.

```
-mods=1163881
```

Multiple mods are comma separated with no spaces:

```
-mods=1163881,927131,893657
```

A full ASA server launch line ends up looking something like this:

```batch
ArkAscendedServer.exe TheIsland_WP?SessionName="My Modded Server"?MaxPlayers=20?ServerAdminPassword=changeme -port=7777 -WinLiveMaxPlayers=20 -mods=1163881
```

The server downloads and updates the listed mods itself on startup, so you do not need to fetch anything manually or run SteamCMD against mod IDs.

A few ASA-specific quirks that catch people out:

* `?ServerAdminPassword=` has to be the **last** option using the `?` syntax. Anything after it gets parsed as part of the password.
* ASA needs `-port=<port>` with a dash, not `?Port=`. Using the `?` form silently leaves you on 7777.
* `ActiveMods` in `GameUserSettings.ini` is an ASE thing and is ignored by ASA. Use `-mods=` instead.

**NOTE** - If you are setting up an ASA server from scratch, our separate [ARK: Survival Ascended server guide](https://moddingcommunity.com/blog/how-to-setup-an-ark-survival-ascended-server/) covers SteamCMD, ports and configuration.

## The TMC App
Worth a mention even though ASA needs it least of any game we write these guides for. [The TMC App](https://moddingcommunity.com/tmc-app) is our own mod manager and server browser, and since ASA installs its own mods through the in-game browser, the parts that matter here are the other ones: a **server browser** with real-time latency and status graphs, filtering by game version and mod list, and **RCON** with full command history, commands sent to several servers at once, and commands scheduled for later.

**ARK: Survival Ascended is not in its supported games list**, and for mod deployment it probably never needs to be. The server-side features are the useful half for this game.

**The app is in very early development**, which its README states outright, so treat anything it does as partially tested for now. Trying it and telling us what broke is genuinely the most valuable thing anyone can contribute at this stage.

It is **open source** under GPL-3.0 at [github.com/modcommunity/tmc-app](https://github.com/modcommunity/tmc-app). Bugs and feature requests go in [the issue tracker](https://github.com/modcommunity/tmc-app/issues), and pull requests are welcome.

Installing it:

* **Linux**: one line, no root and no package manager.

```bash
curl -fsSL https://raw.githubusercontent.com/modcommunity/tmc-app/main/scripts/install.sh | sh
```

* **Windows**: the `setup.exe` or `setup.msi` from the [releases page](https://github.com/modcommunity/tmc-app/releases). There is a portable build too, though it does not register the launcher entry or the `tmc://` link handler.
* **macOS**: the `.dmg` from the same releases page.

## Mod Load Order
Order matters when two mods change the same thing, and in ASA the order is the order you list them in.

On a server, the leftmost ID in `-mods=` has the highest priority, and mods further right are overridden by those to their left. If you are running a custom map alongside content mods, the map normally goes first.

In single player, the in-game mod list is the order, and you can rearrange it there.

If two mods change the same creature or the same structure, you will get whichever one wins the order rather than a merge. There is no conflict detection, so mod descriptions and the mod's own comments are your best guide to what plays nicely with what.

## Configuring Mods
Most ASA mods that have settings expose them through `GameUserSettings.ini` or `Game.ini`, in their own named section. The mod's CurseForge description is the documentation, and there is no standard here.

Better Horde Mode is a good example of a mod that does this properly: it ships a full settings document and its source is on GitHub, so you can see exactly what each option does.

On a single player world, those `.ini` files live under your ASA save folder. On a server, they are under `ShooterGame/Saved/Config/`.

## Updating And Removing Mods
Updates happen on their own. The game checks for new mod versions when you launch and when you join a server, and the server does the same on startup. You do not need to do anything.

That is convenient and occasionally annoying, since a mod update can arrive mid-playthrough and change balance under you. Server owners who need stability tend to run a fixed mod list and test updates on a copy first.

To remove a mod, uninstall it in the in-game **Mods** menu, or take its ID out of your server's `-mods=` list.

**WARNING** - As mentioned above, removing a content mod from a world that used it will usually damage that save. Decide before you start a long playthrough rather than after.

## Troubleshooting
**A mod will not download.** CurseForge's CDN occasionally rate limits or stalls. Restart the game and try again before assuming anything is broken.

**Stuck on "downloading mods" when joining a server.** Usually just a big mod list on a slow connection. Give it real time. If it genuinely hangs, restart the game and rejoin.

**The mod installed but nothing changed in-game.** Check it is actually enabled in the mod list, and that you started a new session after enabling it. Some mods only take effect on a fresh world.

**Server starts but mods do not load.** Check you used `-mods=` rather than `ActiveMods`, that the IDs are Project IDs and not file IDs, and that there are no spaces after the commas.

**Two mods conflict.** Reorder them. The one you want to win goes further left in `-mods=`, or higher in the single player list.

**Save is broken after removing a mod.** Restore your backup. There is no clean repair for this.

**Running on Linux via Proton.** ASA has no native Linux client, and the same applies to the dedicated server. Both need Proton or Wine. Expect this to be rougher than a native setup.

## Conclusion
ASA modding is the least fiddly system in this whole set of guides. There is no mod loader, no folder to manage and no manual downloads. Open the **Mods** menu, install what you want, and play. Joining a modded server does not even need that much, since the game fetches everything for you.

The two things actually worth knowing are Project IDs, which are what server owners and support threads speak in, and the fact that removing a content mod from a world will normally break that world. Back up before you experiment.

If you run servers as well as play on them, the [TMC App](https://github.com/modcommunity/tmc-app) is open source, early in development, and feedback on its server browser and RCON would be appreciated.

## See Also
* [ARK: Survival Ascended on CurseForge](https://www.curseforge.com/ark-survival-ascended)
* [Official ARK Discord](https://discord.com/invite/playascended)
* [ARK Wiki: Survival Ascended](https://ark.wiki.gg/wiki/ARK:_Survival_Ascended)
* [ARK Wiki: Server configuration](https://ark.wiki.gg/wiki/Server_configuration) - The full reference for every launch option and `.ini` setting.
* [TMC App](https://github.com/modcommunity/tmc-app)

We keep this guide as current as we can, but ARK and CurseForge both change over time. If you find an instruction that no longer matches what you are seeing, please report it or open a [pull request](https://github.com/modcommunity/how-to-install-mods-in-ark-se/pulls) on this guide's GitHub repository.

Join our [Discord server](https://discord.moddingcommunity.com) if you have any questions or want help with anything modding related!
