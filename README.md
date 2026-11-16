# RimThreaded Overclocked - tester build

Test copy of **RimThreaded Overclocked**, an unofficial continuation of RimThreaded (multithreading for RimWorld), for
friends who test it. Thank you for helping. This is its own mod (`drpepper.rimthreaded.overclocked`).

- **Current build: 144** (see [CHANGELOG.md](CHANGELOG.md)). Tested on RimWorld **1.7** (1.7.5005). The 1.6 files are included but were not retested for this build.
- **Back up your saves first.** This is a test build.
- Based on RimThreaded by Caleb Seelhoff (Major Hoff, MIT license) and the 1.6 port by kazenokizu. They do not make or support this version: report problems to the owner of this repo, not to them.

## Install
1. Close RimWorld. Download the zip from **Releases** (or clone this repo) and copy the `RimThreaded` folder into RimWorld's `Mods` folder, so you have `Mods/RimThreaded/About/About.xml`.
2. **Remove or disable the original RimThreaded** (`majorhoff.rimthreaded`). Never run both.
3. Start the game, enable **RimThreaded Overclocked**, and put it **right after Harmony/Core and before other mods** in the load order.
4. Mod settings > RimThreaded Overclocked: set the number of threads to about the number of **CPU cores** (not threads). More than your cores is slower.
5. To update later: close the game, replace the whole `RimThreaded` folder with the new one.

## What to try
Play normally and watch for: errors in red, freezes, pawns standing still, saves that fail to load, or the game being slower than without the mod. To compare, turn the mod off (the game must restart) and play the same save.

## Not compatible (do not run together)
- The original RimThreaded, RocketMan, Multiplayer, Prepatcher, Time Control.
- IsoRimZ (breaks map generation).
- Older original-list mods: Dreamer's Dream, Pawnmorpher, RimUhiversi, Turn It On and Off, Biomes! Islands, Terrain Movement Modkit, Prisoner Arena, Doors Expanded, Windows.

Known small limits: Mining Priority (Continued) options have no effect; Smarter Construction builds in vanilla order; Humanoid Alien Races with their own atlas scale can look the wrong size when zoomed far out.

Broken on 1.7 with or without this mod (ask the mod author): Biomes! Core and add-ons, Fortifications - Industrial, Castle Walls Expanded, Nivarian Race, Mechalit Faction 2, Xeva Faction, Argonic Core, Outer Rim Core, Elite Bionics Framework, Control Bar Plus (2026-11-13 update), and Combat Extended with weapon packs that have no CE patch.

## Reporting a problem
Send the owner: your RimWorld version, your mod list (`Config/ModsConfig.xml`), what you did, what you expected, and the log (`Player.log`; in-game: dev mode > open log, or the mod's one-click bug report, which removes your names). Say whether it also happens with the mod switched off.

## Switches (advanced)
Launch options such as `-rtmodfixes=off` (turns off the built-in fixes for other mods), `-rtframepacing=off`, `-rtfleckframe=off` switch single features off if one misbehaves; tell the owner which one helped.

## License
MIT, see [LICENSE](LICENSE). This is a test build: please link to this repo instead of re-uploading the files to the Steam Workshop or other sites, so everyone gets the latest build.
