# Netherite Finder V1 — 1.1.0

Netherite Finder V1 **1.1.0** — offhand XP repair, F6 controls, lava detours, storage capacity, cameras and loaded base clues.

**[Download netherite-finder-v1-1.1.0.jar](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.1.0.jar)**

Replace the previous Finder JAR; keep one version in `mods`. **Minecraft 1.21.11 / Fabric Loader 0.19.3+ / Java 21**. Fabric API is bundled unchanged. This is the standalone Finder; the cancelled Netherite Client is not part of this release.

### Controls and changes

- **F6** opens the redesigned, resolution-scaled menu with **MINER**, **ESP/CHEATS** and **AUTO BASE FINDER** categories plus scrollable instructions. The new binding ID prevents saved F7/F8 defaults from overriding F6.
- **XP repair puts the Mending pickaxe in the OFFHAND and throws bottles from the MAIN HAND.** It stays equipped during XP collection. Repair completion, OFF, missing bottles or opening a menu restore the previous offhand item with paced inventory swaps. The offhand totem is temporarily displaced; an abrupt disconnect can prevent the final swap, so check your inventory after reconnecting.
- **Lava does not switch mining OFF.** The bot plugs encountered lava using plain hotbar blocks, waits for real placement confirmation, and uses a short walking/digging detour if plugging fails. It tries to swim to a safe loaded shore if already in lava. Lava is still dangerous; keep blocks and spare totems stocked.
- **No 64-item storage threshold.** It fills usable player storage, deposits into a real ender chest, continues into remaining player space if the ender chest fills, and stops when both are full. Tools, supplies and one hotbar building stack are protected. Recheck storage after manually emptying the chest.
- Direct approaches, eased bounded turns, held waypoints, checked diagonals and local recovery are retained. Clear straight corridors can use normal sprinting. Mining obeys the tool's actual speed and reach.
- **F4 freecam** moves the render camera with WASD / Space / Shift. Idle manual movement leaves the body still; active automation may continue moving the body. **Z freelook** orbits without terrain clipping and turns the camera without turning the body. Both can be disabled, with configurable camera speed and orbit distance.
- Debris ESP is independently switchable. Preferences persist in `config/netherite-finder.json`; automation/cameras reset OFF on disconnect.
- **AUTO BASE FINDER** scans loaded underground storage clusters, digs toward them, opens accessible containers to inspect real contents, skips apparently raided empty clusters, and stops with coordinates when storage contains items. It never takes contents. Minimum storage count, search depth and a rescan control are included.
- Base targets within **30 blocks of loaded trial spawners or vaults** are excluded. Loaded storage is a clue, not proof of a player base; unseen chambers, unloaded bases and server-hidden data cannot be detected. Inaccessible storage is treated as unknown.

### Validation and limits

Build/contracts and **14 actual local Minecraft checks** pass using the final remapped JAR: F6 categories/instructions; real lava plug/mining/pickup; external-drop pickup; chest-obstruction recovery; lava detour with no hotbar blocks; server-confirmed offhand Mending and restoration; real totem pop/refill with the menu open; no early deposit at 64; actual 1,728-debris ender transfer; stopping at full player+ender storage; independent F4/Z cameras and camera disable control; trial exclusion; empty-cluster inspection followed by another base with actual loot; loaded-player radius/logout.

Tests run in a disposable local Linux/Mesa survival world. Storage stacks and test containers are provided by the test fixture. No public server is modified. ClamAV 1.5.4 scanned the complete final JAR: **zero detections**. This is not Microsoft Defender certification. Server permissions, anti-cheat compatibility, Windows hardware, arbitrary lava layouts and hidden world/player data are not guaranteed. Use automation where permitted.

- [Source and build instructions](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.1.0-source.zip)
- [SHA-256 checksums](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/SHA256SUMS-netherite-finder-v1-1.1.0.txt)
- [Scan report](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/SCAN-REPORT-netherite-finder-v1-1.1.0.txt)
- [F6 menu preview](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.1.0-menu.png)

# Netherite Finder V1 — 1.1.0

Minecraft Java **1.21.11**, **Fabric Loader 0.19.3+**, **Java 21**. This is the standalone Finder, independent of Astra and Crystal. Fabric API 0.141.6+1.21.11 is bundled unchanged as a Fabric nested JAR.

## Install

Replace the previous Finder JAR with `netherite-finder-v1-1.1.0.jar` in the Fabric instance's `mods` folder; keep only one Finder version. Press **F6** in game. Controls have three categories: **MINER**, **ESP/CHEATS**, **AUTO BASE FINDER**. Choose a mode, switch ON, then close the menu. Automation and cameras start OFF and never resume automatically after reconnecting.

**You must have XP bottles in your inventory and a good diamond/netherite pickaxe.** Mending enables automatic repair; Efficiency and Unbreaking help. Carry spare Totems of Undying, an ender chest, and plain netherrack, basalt or blackstone **in the hotbar** for lava plugs and supported steps. Silk Touch enables recovery of a placed ender chest.

## Mining, lava and storage

The miner scans loaded Nether chunks incrementally, highlights real ancient-debris states red, takes direct checked tunnel steps, and walks to dropped debris until inventory pickup is confirmed. It measures actual movement/mining progress, holds waypoints until reached, uses short look-ahead and checked diagonals, and takes bounded local walking/digging detours around obstacles. Turns use damped easing and bounded angular speed. Clear aligned corridors can use normal Minecraft sprinting. Mining still obeys real tool speed and reach.

Lava does not switch automation OFF. The miner tries actual block placements **from hotbar building stacks**, waits for confirmation, then tries a short safe detour if placement is impossible or rejected. An unreachable target is temporarily excluded and exploration changes direction. If already in lava it tries to swim upward toward a loaded safe shore. Hidden/flowing lava can still hurt or kill the player; this is not invulnerability.

There is **no 64-debris deposit threshold**. Debris fills usable player slots first, including slots freed by removing expendable mining blocks, while protecting gear, supplies and one hotbar building stack. At capacity it opens or places a real ender chest and transfers debris. If the ender chest fills it continues using freed player space, stopping when both are full. The menu's **Recheck ender-chest capacity** clears remembered fullness after you manually make room. A placed chest is recovered with Silk Touch; otherwise it is left in place. Missing supplies or rejected interactions can pause a task.

Only plain netherrack, basalt, blackstone, gravel, soul sand and soul soil may be discarded. Named, enchanted, lore-bearing or custom-data items are excluded, as is one reserved hotbar building stack. It never discards tools, totems, XP bottles, ender chests or debris. Capacity refers to available storage after these protections, rather than replacing your equipment with debris.

## Mending and auto totem

At 70% remaining tool durability, repair places the Mending pickaxe **in the OFFHAND** and throws real XP bottles **from the MAIN HAND**. The pickaxe stays equipped throughout XP flight and collection, until roughly 92% durability. Repair consumes supplied bottles and other damaged Mending gear can share XP.

The previous offhand item is restored with normal inventory swaps when repair completes, XP runs out, you turn OFF, or you open a menu. The offhand totem is temporarily displaced during repair. An abrupt disconnect can prevent restoration: check your inventory after reconnecting. If no safe slot is available, restoration waits without dropping gear.

Outside that repair session, auto totem equips a spare after a consumed offhand totem, including while the F6 menu is open. No spare after a pop stops automation. Container actions are paced normal Minecraft clicks; server inventory rules still apply.

## ESP / cameras

- **Ancient debris ESP** is independently switchable and only displays server-sent loaded blocks.
- **F4** toggles render-only freecam. WASD, Space and left Shift move the camera smoothly. The physical player stays still from those inputs while automation is OFF. With automation ON the bot can continue moving the body. Camera movement is limited to 96 blocks from the body and does not load remote chunks.
- **Z** toggles collision-free orbit freelook. Mouse input turns the camera without turning the player's body; the orbit may pass through loaded terrain. This does not expose server-hidden/unloaded blocks.
- Both camera features can be disabled in **ESP/CHEATS**, and camera speed/orbit distance are configurable. Toggling again restores the normal camera; disconnect resets both.

Preferences are saved in `config/netherite-finder.json`. Keybinds can also be changed through Minecraft Controls.

## Auto Base Finder

This separate mining mode scans only loaded underground chest, trapped-chest, barrel and shulker storage clues. It requires the configured minimum number of storage blocks in a nearby cluster and digs toward an accessible container. It opens actual containers, waits for real server contents, and stops with coordinates when storage contains items. It never takes contents.

After accessible storage in a cluster is checked and empty, it treats the cluster as apparently raided and searches in another direction. Locked or inaccessible storage is unknown and skipped, rather than called empty. Natural structures can resemble a base; this is a heuristic, not proof of an occupied player base.

Targets within **30 blocks of a loaded trial spawner or vault** are excluded. Loaded neighbouring block entities are checked before selecting or approaching targets. Entire unseen trial chambers cannot be identified by a client. Search depth, minimum storage count, and a rescan/reset control are available in its category.

## Existing safeguards and limits

Another loaded, non-spectator player within **128 horizontal blocks (8 chunks)** triggers a normal logout and disables automation. Entity tracking and anti-xray can prevent a client from seeing players or ore. Menus pause movement/mining, except the mod's own storage-inspection tasks. OFF releases inputs, and pending offhand restoration can finish while OFF. Death, unsafe falling and exhausted storage stop automation.

The mod takes over movement, aiming, mining and the described inventory actions while ON. Monitor supplies and terrain. Server protection, latency and inventory rules may reject actions. There is no anti-cheat bypass, guarantee against flags, guaranteed base detection or guarantee against lava. Use automation only where permitted.

## Build and inspection

With Java 21, run `./gradlew build` (`gradlew.bat build` on Windows). The installable remapped JAR is `build/libs/netherite-finder-v1-1.1.0.jar`. Contract tests are under `tools/tests`. The external native observer and its disposable test world are excluded from release files.

Bundled Fabric API is unchanged and licensed Apache-2.0; its license is in `META-INF/licenses` and `vendor/Fabric-API-LICENSE.txt`. Upstream: https://github.com/FabricMC/fabric . No operating-system helpers, browser engines or executable installers are included. Antivirus scan results identify the exact release bytes and are not Microsoft Defender certification.
