# Netherite Finder V1 — 1.1.2

Netherite Finder V1 **1.1.2** adds faster debris approaches using ordinary Minecraft movement.

**[Download netherite-finder-v1-1.1.2.jar](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.1.2.jar)**

Replace the old Finder JAR in `mods`; keep one version. **Minecraft Java 1.21.11 / Fabric Loader 0.19.3+ / Java 21**. Fabric API is bundled unchanged. **F6** opens controls; **F4** freecam and **Z** freelook are retained.

### Faster approach

- **Fast approach is ON by default**, with an ON/OFF button in MINER. The actual menu toggle and saved preference are tested.
- Long open approaches can use ordinary **sprint-jumps** after checking a full five-block flat landing corridor, loaded terrain, headroom, hunger and alignment. The bot does not jump in tight tunnels, close to the target, across unknown floors or beside detected lava.
- A jump keeps its checked heading instead of chasing block centres in mid-air, and the bot lands before mining. The timing runs recorded **zero airborne attack ticks**.
- When a valid native crosshair is mining a block, the bot can walk closer across checked supported ground. This overlaps the remaining approach with mining and reduces the later pickup walk.
- Faster critically damped mining aim reduces settling delays without snapping. Normal sprinting continues across waypoint centres with a stopping margin near the target.
- A restart clears a stale route-retry wait. Existing lava recovery, offhand Mending/totem restoration, storage, base clues and logout behaviour remain.

**No movement attribute, velocity, reach, tick rate or tool break speed is increased.** Tool quality, hunger, geometry, server timing and permissions still apply. Fast approach OFF disables the new sprint-jumps and closing-in-while-mining behaviour.

### Measured locally

Three repeats per version and lane, with an Efficiency V netherite pickaxe, a 28-block flat approach and fixed supplies, measured in game ticks:

| Fixture | 1.1.1 median | 1.1.2 median | Less time |
| --- | ---: | ---: | ---: |
| Open route: approach to first ore hit | 91 | 76 | 16.5% |
| Open route: full mine and pickup | 134 | 114 | 14.9% |
| Two-high pre-dug tunnel: full mine and pickup | 135 | 130 | 3.7% |

The open lane used normal sprint-jumps; the low tunnel stayed grounded. Every candidate run confirmed real server-side debris collection. These are controlled local Linux/Mesa Minecraft results, not a universal speed or FPS promise. Raw samples are provided below.

### Validation

Build/contracts, **18 native movement and retained-feature checks**, and six candidate timing runs pass. Six matching baseline runs are included. Checks cover the Fast approach toggle, real lava plugs and pickup, external drops, chest recovery, clear paths at several angles, inventory-only blocks, immersed lava recovery, offhand XP repair, totem refill, full usable/ender storage, base inspection/trial exclusion and nearby-player logout. Camera code is unchanged from 1.1.1 and was not re-tested for this movement update.

Tests use an isolated local world; no public server is modified. The lava fixture supplies Fire Resistance only for deterministic testing, not as a release feature. ClamAV 1.5.4 scanned the complete final JAR: **zero detections**. This is not Microsoft Defender certification or an anti-cheat guarantee. Server-hidden blocks/players and server permissions still limit the client. Use automation where permitted.

- [Source and build instructions](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.1.2-source.zip)
- [SHA-256 checksums](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/SHA256SUMS-netherite-finder-v1-1.1.2.txt)
- [Scan report](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/SCAN-REPORT-netherite-finder-v1-1.1.2.txt)
- [F6 menu preview](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.1.2-menu.png)
- [Raw benchmark samples and comparison](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/BENCHMARK-netherite-finder-v1-1.1.2.json)

# Netherite Finder V1 — 1.1.2

Minecraft Java **1.21.11**, **Fabric Loader 0.19.3+**, **Java 21**. This is the standalone Finder, independent of Astra and Crystal. Fabric API 0.141.6+1.21.11 is bundled unchanged as a Fabric nested JAR.

## Install

Replace the previous Finder JAR with `netherite-finder-v1-1.1.2.jar` in the Fabric instance's `mods` folder; keep only one Finder version. Press **F6** in game. Controls have three categories: **MINER**, **ESP/CHEATS**, **AUTO BASE FINDER**. Choose a mode, switch ON, then close the menu. Automation and cameras start OFF and never resume automatically after reconnecting.

**You must have XP bottles in your inventory and a good diamond/netherite pickaxe.** Mending enables automatic repair; Efficiency and Unbreaking help. Carry spare Totems of Undying, an ender chest, and plain building blocks for lava plugs and supported steps. Hotbar blocks are preferred; the miner can bring suitable blocks from the main inventory into the hotbar. Supported materials are netherrack, basalt, blackstone, cobblestone, cobbled deepslate, stone, deepslate, dirt and end stone. Silk Touch enables recovery of a placed ender chest.

## Faster approach

**Fast approach is ON by default** and can be toggled in the MINER category. It uses ordinary Minecraft sprinting, and can use normal sprint-jumps on long, flat approaches only after checking a full five-block landing corridor and enough headroom. It does not jump through low tunnels, over unknown floors, toward nearby targets, or beside detected lava. It keeps the checked heading during the jump and lands before starting to mine.

While a real native crosshair mines a visible block, the bot can walk closer across checked supported ground. This overlaps approach and mining rather than standing at maximum reach and then walking the entire pickup gap. Mining aim uses faster critically damped tracking, without snapping. Regular tool hardness, reach, durability, hunger and server timing still apply. No movement attributes, velocity, tick rate or reach are increased. Turning Fast approach OFF disables sprint-jumps and closing the distance while mining.

In three repeats of each isolated 28-block fixture, the median open-route approach-to-first-hit time fell from **91 to 76 game ticks**, and the full mine/pickup cycle from **134 to 114 ticks**. A two-high pre-dug tunnel remained grounded: its full cycle fell from **135 to 130 ticks**. These are local Minecraft 1.21.11/Mesa tests with an Efficiency V netherite pickaxe and fixed supplies, not a promise for every terrain, tool, server or network connection. See the benchmark report for the raw samples.

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

With Java 21, run `./gradlew build` (`gradlew.bat build` on Windows). The installable remapped JAR is `build/libs/netherite-finder-v1-1.1.2.jar`. Contract tests are under `tools/tests`. The external native observer and its disposable test world are excluded from release files.

Bundled Fabric API is unchanged and licensed Apache-2.0; its license is in `META-INF/licenses` and `vendor/Fabric-API-LICENSE.txt`. Upstream: https://github.com/FabricMC/fabric . No operating-system helpers, browser engines or executable installers are included. Antivirus scan results identify the exact release bytes and are not Microsoft Defender certification.
