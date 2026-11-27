# Netherite Finder V1 — 1.0.2

Netherite Finder V1 **1.0.2** smooths movement and adds recovery from stalls and obstructions.

**[Download netherite-finder-v1-1.0.2.jar](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.0.2.jar)**

Replace the old Netherite Finder JAR; keep only one version. **Minecraft 1.21.11 / Fabric Loader 0.19.3+ / Java 21**. Fabric API is included. **F7** opens the controls.

### Changed

- Eased camera turns with bounded turn rates and smooth stops, including shortest-angle turning across the rotation boundary.
- Waypoints are held until reached, preventing premature turns at block edges and stair steps.
- Clear corridors use a short look-ahead; open spaces allow checked diagonal walking. Walking uses normal Minecraft inputs and speed.
- Actual progress is measured while moving. Mining, menus and expected block-placement waits do not count as a stall.
- If obstructed, a short local recovery route can step around a nearby chest or blocked corner. Recently failed waypoints are remembered so the same spot is not immediately retried.
- Recovery uses checked supported positions, has a limited number of attempts, and stops with an explanation if there is no safe nearby route.

The 1.0.1 pickup fix, direct approach, inventory lava plugs, auto totem (including in the F7 menu), XP repair, 64-debris ender-chest storage and loaded-player logout are retained.

### Validation

The final JAR passes build/contracts and eight actual local Minecraft checks: F7 controls/highlighting; mining with a real lava plug and pickup; walking to an externally broken debris drop six blocks away; recovery around a chest obstruction followed by pickup; Mending repair; a real totem pop/refill with F7 open; server-confirmed 64-debris ender-chest transfer; and loaded-player radius/logout. Native movement checks bound the camera turn rate, and contract checks cover smoothing, angle wraparound, stall detection and local recovery.

ClamAV 1.5.4 scanned the final JAR with zero detections. This is not Microsoft Defender certification. Tests use an isolated Linux/Mesa local world, with no public server modified. Server-hidden ore/players cannot be revealed, and no anti-cheat compatibility or lava-safety guarantee is made. Use automation where permitted.

- [Source and build instructions](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.0.2-source.zip)
- [SHA-256 checksums](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/SHA256SUMS-netherite-finder-v1-1.0.2.txt)
- [Scan report](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/SCAN-REPORT-netherite-finder-v1-1.0.2.txt)
- [F7 menu preview](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.0.2-menu.png)

# Netherite Finder V1

Minecraft Java **1.21.11**, **Fabric Loader 0.19.3+**, **Java 21**.
Fabric API is included as an unchanged Fabric nested JAR. This is a new
mod, independent of Crystal Client and Astra Client.

## Install and start

Put `netherite-finder-v1-1.0.2.jar` in your Fabric instance's `mods` folder.
Enter the Nether, press **F7**, choose **ON**, and close the menu. The same
menu has scrollable instructions and an OFF control. F7 also closes it.
Automation starts OFF and stays OFF after disconnect/reconnect.

**You must have XP bottles in your inventory and a good pickaxe.**
Use a diamond/netherite pickaxe with **Mending** for automatic repair;
Efficiency and Unbreaking help. Carry spare Totems of Undying and an
ender chest. **Silk Touch** allows recovery of a placed ender chest.

## Implemented behavior

- A bounded, incremental scan searches loaded Nether chunks for actual
  ancient-debris block states. A red, full-bright outline and translucent
  glow remain visible through terrain while ON.
- The miner takes immediate direct tunnel steps toward ancient debris, using normal Minecraft movement, aim, reach and attack inputs.
- Camera turns ease in and out with bounded turn rates. Waypoints are held
  until reached, clear corridors use a short look-ahead, and open spaces
  allow checked diagonal walking. These changes reduce block-by-block
  stops and abrupt turns without changing Minecraft movement speed.
- Actual progress is checked while walking. A short nearby detour can
  recover from corners or solid obstructions such as a chest. Recovery is
  bounded and only uses checked supported positions; if there is no safe
  route or repeated recovery fails, the mod stops with an explanation.
- When lava is encountered, it places plain netherrack, basalt or blackstone from your inventory, waits for the block to appear, then continues. It can place supported floor steps where needed. Supply building blocks; it pauses if a safe placement cannot be made.
- Dropped debris takes priority over new ore and routine repair. Actual item positions are followed, including drops created while tunnelling or already on the ground. Collection is confirmed by inventory changes before a new target is chosen. Progress extends the pickup wait; an unsuccessful pickup pauses the miner at the drop.
- When no reachable debris is known, it branch-mines toward Y15 so more
  terrain can be searched. A compact HUD shows the current action.
- Below 70% pickaxe durability, it throws actual XP bottles at paced
  intervals and holds the Mending pickaxe again to collect the orbs.
  Repair continues to roughly 92% durability. XP is consumed from your
  bottles; it is not generated. Other damaged Mending equipment can share
  XP. A lack of repair progress stops the miner; a nearly broken tool is
  protected from further mining.
- Auto totem stays active while ON, including in the F7 menu. A spare totem is equipped after the offhand totem is consumed, using a
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
- User-opened menus pause mining and movement while auto totem remains active. Its own ender-chest menu
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
installable remapped JAR is `build/libs/netherite-finder-v1-1.0.2.jar`.
The source includes route contract tests. The external native test observer
and its local world are excluded from release files.

The bundled Fabric API **0.141.6+1.21.11** is distributed unchanged under
Apache-2.0. Its license is in `META-INF/licenses` inside the JAR and in
`vendor/Fabric-API-LICENSE.txt` in the source. Original project/source:
https://github.com/FabricMC/fabric . No operating-system helpers, browser
engines or executable installers are included.
