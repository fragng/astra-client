# Netherite Finder V1 — 1.1.1

Netherite Finder V1 **1.1.1** fixes unnecessary route changes and freecam controls, improves inventory lava recovery, and adds a camera view-distance request.

**[Download netherite-finder-v1-1.1.1.jar](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.1.1.jar)**

Replace your old Finder JAR in `mods`; keep one version. **Minecraft Java 1.21.11 / Fabric Loader 0.19.3+ / Java 21**. Fabric API is bundled unchanged. **F6** opens the menu, **F4** toggles freecam and **Z** toggles freelook.

### Changed

- **Fixed false obstructions and missed waypoints.** Sprinting can cross a waypoint without a tick landing on its exact centre. Progress now uses the travelled segment and the correct lane/floor, so passing a centre does not trigger an unnecessary detour. Player-sized collision and actual support checks replace the overly strict four-corner floor requirement. A clear path is centred locally before trying another route, and confirmed clear corridors can rejoin direct travel.
- Direct movement, normal sprinting in checked corridors, damped turns and real tool mining speed remain. Newly enabled mining immediately refreshes the closest loaded chunk. No globally optimal route or anti-cheat bypass is claimed.
- **Freecam A/D strafe directions are corrected relative to the view.** Diagonal motion stays normalised.
- **Scroll-wheel freecam speed: 0.25×–4×**, shown in the action bar. Scrolling changes camera speed without changing the selected hotbar slot. The multiplier is also available in ESP/CHEATS and is saved.
- **Lava plugs use suitable blocks from the main inventory when needed**, preferring hotbar supplies. Plain netherrack, basalt, blackstone, cobblestone, cobbled deepslate, stone, deepslate, dirt and end stone are supported; named/customised items are protected.
- **While immersed in lava**, the bot attempts real supported placements into nearby lava outside the player's body while swimming toward a loaded safe shore. It waits for placement confirmation and keeps automation enabled. This does not grant Fire Resistance or invulnerability; hidden/flowing lava and missing supplies remain dangerous.
- **Freecam and freelook temporarily request a larger view distance:** 20 chunks by default, adjustable from 12 to 32 in ESP/CHEATS. Your original render distance is restored on exit. Switching between camera modes retains the temporary boost. Larger view distances use more memory and rendering work.
- **Multiplayer limits still apply.** The request is sent through Minecraft's real client settings; servers decide how many chunks they send around the actual player. Camera modes cannot force remote/server-hidden chunks to load or move the server's streaming centre to the camera.

The previous offhand XP repair/restoration, full usable storage/ender-chest handling, totem refill, debris pickup, loaded storage-clue Base Finder, trial exclusions and nearby-player logout are retained.

### Validation

Build/contracts and **21 actual local Minecraft checks** pass on the final remapped JAR. New checks cover straight, equal-diagonal and unequal-diagonal debris routes without false detours; main-inventory cobblestone lava plugging; block placement and escape while immersed; actual A/D camera movement; real scroll events with speed limits and unchanged hotbar selection; and a larger view-distance request received by the server, followed by restoration on exit. Existing storage, Mending, totem, base inspection and logout checks also pass.

Tests use an isolated local Linux/Mesa survival world. The immersed-lava fixture supplies Fire Resistance only for deterministic testing; the release does not grant it. The local server caps chunk delivery at six while receiving a larger camera request, so unlimited or remote chunk loading is not claimed. Storage stacks and test containers are supplied by the fixture. No public server is modified.

ClamAV 1.5.4 scanned the complete final JAR with **zero detections**. This is not Microsoft Defender certification. Server permissions, anti-cheat compatibility, Windows hardware and arbitrary terrain/lava layouts are not guaranteed. Use automation where permitted.

- [Source and build instructions](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.1.1-source.zip)
- [SHA-256 checksums](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/SHA256SUMS-netherite-finder-v1-1.1.1.txt)
- [Scan report](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/SCAN-REPORT-netherite-finder-v1-1.1.1.txt)
- [F6 menu preview](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.1.1-menu.png)

# Netherite Finder V1 — 1.1.1

Minecraft Java **1.21.11**, **Fabric Loader 0.19.3+**, **Java 21**. This is the standalone Finder, independent of Astra and Crystal. Fabric API 0.141.6+1.21.11 is bundled unchanged as a Fabric nested JAR.

## Install

Replace the previous Finder JAR with `netherite-finder-v1-1.1.1.jar` in the Fabric instance's `mods` folder; keep only one Finder version. Press **F6** in game. Controls have three categories: **MINER**, **ESP/CHEATS**, **AUTO BASE FINDER**. Choose a mode, switch ON, then close the menu. Automation and cameras start OFF and never resume automatically after reconnecting.

**You must have XP bottles in your inventory and a good diamond/netherite pickaxe.** Mending enables automatic repair; Efficiency and Unbreaking help. Carry spare Totems of Undying, an ender chest, and plain building blocks for lava plugs and supported steps. Hotbar blocks are preferred; the miner can bring suitable blocks from the main inventory into the hotbar. Supported materials are netherrack, basalt, blackstone, cobblestone, cobbled deepslate, stone, deepslate, dirt and end stone. Silk Touch enables recovery of a placed ender chest.

## Mining, lava and storage

The miner scans loaded Nether chunks incrementally, highlights real ancient-debris states red, takes direct checked tunnel steps, and walks to dropped debris until inventory pickup is confirmed. It measures actual movement/mining progress, holds waypoints until reached, uses short look-ahead and checked diagonals, and takes bounded local walking/digging detours around obstacles. Turns use damped easing and bounded angular speed. A waypoint counts as reached when safely crossed, even if sprinting skips its exact centre. Movement clearance uses the actual player-sized collision box and floor contact, instead of insisting on a full block under all four corners. A missed centre is corrected locally rather than immediately abandoning the ore. Clear aligned corridors can use normal Minecraft sprinting. Mining still obeys real tool speed and reach.

Lava does not switch automation OFF. The miner tries actual block placements **from available building stacks, preferring the hotbar**, waits for confirmation, then tries a short safe detour if placement is impossible or rejected. An unreachable target is temporarily excluded and exploration changes direction. If already in lava it tries to plug reachable nearby lava outside the player’s body while swimming upward toward a loaded safe shore. It uses real inventory block placements and checks that the server confirms them. It never places a block inside the player. Hidden/flowing lava can still hurt or kill the player; this is not invulnerability.

There is **no 64-debris deposit threshold**. Debris fills usable player slots first, including slots freed by removing expendable mining blocks, while protecting gear, supplies and one hotbar building stack. At capacity it opens or places a real ender chest and transfers debris. If the ender chest fills it continues using freed player space, stopping when both are full. The menu's **Recheck ender-chest capacity** clears remembered fullness after you manually make room. A placed chest is recovered with Silk Touch; otherwise it is left in place. Missing supplies or rejected interactions can pause a task.

Only plain netherrack, basalt, blackstone, gravel, soul sand and soul soil may be discarded. Named, enchanted, lore-bearing or custom-data items are excluded, as is one reserved hotbar building stack. It never discards tools, totems, XP bottles, ender chests or debris. Capacity refers to available storage after these protections, rather than replacing your equipment with debris.

## Mending and auto totem

At 70% remaining tool durability, repair places the Mending pickaxe **in the OFFHAND** and throws real XP bottles **from the MAIN HAND**. The pickaxe stays equipped throughout XP flight and collection, until roughly 92% durability. Repair consumes supplied bottles and other damaged Mending gear can share XP.

The previous offhand item is restored with normal inventory swaps when repair completes, XP runs out, you turn OFF, or you open a menu. The offhand totem is temporarily displaced during repair. An abrupt disconnect can prevent restoration: check your inventory after reconnecting. If no safe slot is available, restoration waits without dropping gear.

Outside that repair session, auto totem equips a spare after a consumed offhand totem, including while the F6 menu is open. No spare after a pop stops automation. Container actions are paced normal Minecraft clicks; server inventory rules still apply.

## ESP / cameras

- **Ancient debris ESP** is independently switchable and only displays server-sent loaded blocks.
- **F4** toggles render-only freecam. WASD, Space and left Shift move the camera smoothly, with corrected A/D strafe directions relative to the view. The scroll wheel adjusts speed from **0.25× to 4×** and displays the current multiplier; scrolling does not change your hotbar selection. The physical player stays still from those inputs while automation is OFF. With automation ON the bot can continue moving the body. Camera movement is limited to 96 blocks from the body and does not load remote chunks.
- **Z** toggles collision-free orbit freelook. Mouse input turns the camera without turning the player's body; the orbit may pass through loaded terrain. This does not expose server-hidden/unloaded blocks.
- Both camera features can be disabled in **ESP/CHEATS**, and camera speed/orbit distance are configurable. Toggling again restores the normal camera; disconnect resets both.

Camera modes temporarily request **20 chunks of view distance** by default, adjustable from 12 to 32 in ESP/CHEATS. The original render distance is restored on exit, and switching between camera modes retains the temporary boost. Manual changes to render distance are preserved. Larger view distances use more memory and rendering work. Multiplayer servers still control the chunks sent around the actual player position: freecam and freelook cannot force remote or server-hidden chunks to load, or move the server’s chunk-streaming centre away from the player.

Preferences are saved in `config/netherite-finder.json`. Keybinds can also be changed through Minecraft Controls.

## Auto Base Finder

This separate mining mode scans only loaded underground chest, trapped-chest, barrel and shulker storage clues. It requires the configured minimum number of storage blocks in a nearby cluster and digs toward an accessible container. It opens actual containers, waits for real server contents, and stops with coordinates when storage contains items. It never takes contents.

After accessible storage in a cluster is checked and empty, it treats the cluster as apparently raided and searches in another direction. Locked or inaccessible storage is unknown and skipped, rather than called empty. Natural structures can resemble a base; this is a heuristic, not proof of an occupied player base.

Targets within **30 blocks of a loaded trial spawner or vault** are excluded. Loaded neighbouring block entities are checked before selecting or approaching targets. Entire unseen trial chambers cannot be identified by a client. Search depth, minimum storage count, and a rescan/reset control are available in its category.

## Existing safeguards and limits

Another loaded, non-spectator player within **128 horizontal blocks (8 chunks)** triggers a normal logout and disables automation. Entity tracking and anti-xray can prevent a client from seeing players or ore. Menus pause movement/mining, except the mod's own storage-inspection tasks. OFF releases inputs, and pending offhand restoration can finish while OFF. Death, unsafe falling and exhausted storage stop automation.

The mod takes over movement, aiming, mining and the described inventory actions while ON. Monitor supplies and terrain. Server protection, latency and inventory rules may reject actions. There is no anti-cheat bypass, guarantee against flags, guaranteed base detection or guarantee against lava. Use automation only where permitted.

## Build and inspection

With Java 21, run `./gradlew build` (`gradlew.bat build` on Windows). The installable remapped JAR is `build/libs/netherite-finder-v1-1.1.1.jar`. Contract tests are under `tools/tests`. The external native observer and its disposable test world are excluded from release files.

Bundled Fabric API is unchanged and licensed Apache-2.0; its license is in `META-INF/licenses` and `vendor/Fabric-API-LICENSE.txt`. Upstream: https://github.com/FabricMC/fabric . No operating-system helpers, browser engines or executable installers are included. Antivirus scan results identify the exact release bytes and are not Microsoft Defender certification.
