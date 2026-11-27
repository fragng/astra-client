# Netherite Finder V1

Netherite Finder V1 is a separate Minecraft Java **1.21.11 / Fabric Loader 0.19.3+ / Java 21** mod. Fabric API is included in the single installable JAR.

**[Download Netherite Finder V1.jar](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.0.0.jar)**

## Install and use

Put the JAR in your Fabric instance's `mods` folder. Enter the Nether, press **F8**, switch **ON**, and close the menu. F8 opens/closes its controls; the Instructions button explains supplies and behavior.

**You must have XP bottles and a good diamond/netherite pickaxe in your inventory.** Mending is required for automatic repair. Carry spare totems and an ender chest; Silk Touch lets the mod recover its placed chest.

## Included

- Glowing red through-terrain highlighting of loaded ancient-debris blocks.
- Bounded route planning, normal-speed Minecraft movement/aim/mining and debris pickup.
- Known-lava/unsafe-floor avoidance, with branch tunnelling toward Y15 when no reachable debris is known.
- Actual Mending repair using inventory XP bottles, and paced totem replenishment.
- Ender-chest placement/opening and debris deposit at 64+ inventory debris.
- Pickup-space cleanup limited to plain netherrack, basalt, blackstone, gravel, soul sand and soul soil. Named/custom items, supplies and gear are protected.
- Logout when another loaded non-spectator player is within 128 horizontal blocks (8 chunks).
- Compact status HUD, F8 instructions and OFF after disconnect/reconnect.

Server-hidden ore and untracked players cannot be revealed by a client. Lava avoidance cannot guarantee safety, supplies are finite, and no anti-cheat compatibility or flag-free guarantee is provided. Use automation only where permitted.

## Validation

The build/contract checks pass. Actual local survival-world tests verified mining and pickup, lava avoidance, full-inventory cleanup, server-side Mending repair, a real totem pop/refill, a server-confirmed 64-debris ender-chest transfer and loaded-player radius/logout behavior. The observer/world are excluded from the download. The storage test supplies the 64-stack to exercise transfer, rather than claiming a benchmark of mining 64.

ClamAV 1.5.4 scanned the final JAR, including nested archive contents, with 0 infected files. This is not Microsoft Defender certification. Native tests used Linux/X11/Mesa software rendering; no public Minecraft server was connected to or modified.

- [Source and build instructions](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.0.0-source.zip)
- [SHA-256 checksums](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/SHA256SUMS-netherite-finder-v1.txt)
- [Scan report](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/SCAN-REPORT-netherite-finder-v1.txt)
- [Menu preview](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-menu.png)

# Netherite Finder V1

Minecraft Java **1.21.11**, **Fabric Loader 0.19.3+**, **Java 21**.
Fabric API is included as an unchanged Fabric nested JAR. This is a new
mod, independent of Crystal Client and Astra Client.

## Install and start

Put `netherite-finder-v1-1.0.0.jar` in your Fabric instance's `mods` folder.
Enter the Nether, press **F8**, choose **ON**, and close the menu. The same
menu has scrollable instructions and an OFF control. F8 also closes it.
Automation starts OFF and stays OFF after disconnect/reconnect.

**You must have XP bottles in your inventory and a good pickaxe.**
Use a diamond/netherite pickaxe with **Mending** for automatic repair;
Efficiency and Unbreaking help. Carry spare Totems of Undying and an
ender chest. **Silk Touch** allows recovery of a placed ender chest.

## Implemented behavior

- A bounded, incremental scan searches loaded Nether chunks for actual
  ancient-debris block states. A red, full-bright outline and translucent
  glow remain visible through terrain while ON.
- The miner plans a supported two-block-high route, checks it again before
  moving/mining, aims with bounded turns, and uses Minecraft's native
  movement and attack controls. Tool/enchantment mining speed and normal
  block-interaction reach still apply.
- It rejects known lava-adjacent cells, unsafe floors, unbreakable blocks,
  block entities and unloaded routes. It does not dig out the floor under
  the player. Blocked routes are retried with a bounded search.
- When no reachable debris is known, it branch-mines toward Y15 so more
  terrain can be searched. A compact HUD shows the current action.
- Below 70% pickaxe durability, it throws actual XP bottles at paced
  intervals and holds the Mending pickaxe again to collect the orbs.
  Repair continues to roughly 92% durability. XP is consumed from your
  bottles; it is not generated. Other damaged Mending equipment can share
  XP. A lack of repair progress stops the miner; a nearly broken tool is
  protected from further mining.
- A spare totem is equipped after the offhand totem is consumed, using a
  paced normal inventory swap. If no spare remains, automation stops.
- At 64+ ancient debris in the inventory, it opens a visible nearby ender
  chest or places one on a checked floor, waits for the actual chest menu,
  and transfers debris. It checks the transfer result and stops if the
  chest is full or access is rejected. A chest it placed is recovered with
  Silk Touch; without Silk Touch it is left in place.
- To make pickup space, only plain **netherrack, basalt, blackstone,
  gravel, soul sand and soul soil** may be discarded. Named, enchanted,
  custom-data or lore-bearing stacks are excluded. Tools, XP bottles,
  totems, ender chests and debris are never automatic trash. If no allowed
  junk can be removed, clear the inventory manually.
- Another loaded, non-spectator player within **128 horizontal blocks
  (8 chunks)** triggers a normal disconnect and turns the mod OFF.
- User-opened menus pause mining and movement. Its own ender-chest menu
  remains active for the deposit. OFF releases all movement/mining inputs.

## Practical limits

Highlighting and player detection only use data the server has sent to the
client. Anti-xray can hide ancient debris; players outside entity tracking
cannot be detected. Lava can flow or be hidden, so avoidance cannot promise
invulnerability. Region protection, latency and server inventory rules may
reject actions; the mod stops or pauses when an interaction is unconfirmed.
There is no anti-cheat bypass or guarantee against flags. Use automation
only where the server permits it. Supplies and chest capacity are finite.

## Build and inspect

With Java 21, run `./gradlew build` (Windows: `gradlew.bat build`). The
installable remapped JAR is `build/libs/netherite-finder-v1-1.0.0.jar`.
The source includes route contract tests. The external native test observer
and its local world are excluded from release files.

The bundled Fabric API **0.141.6+1.21.11** is distributed unchanged under
Apache-2.0. Its license is in `META-INF/licenses` inside the JAR and in
`vendor/Fabric-API-LICENSE.txt` in the source. Original project/source:
https://github.com/FabricMC/fabric . No operating-system helpers, browser
engines or executable installers are included.
