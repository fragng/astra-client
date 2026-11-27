# Netherite Finder V1 — 1.0.1

Netherite Finder V1 **1.0.1** fixes debris pickup and changes the menu key to **F7**.

**[Download netherite-finder-v1-1.0.1.jar](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.0.1.jar)**

Replace the old Netherite Finder JAR with this one; keep only one version. Requires **Minecraft 1.21.11 / Fabric Loader 0.19.3+ / Java 21**. Fabric API is included.

### Changed

- **Pickup fix:** every actual mined ancient-debris block is tracked, including blocks broken during tunnelling. Nearby dropped debris takes priority. The miner walks to the actual item and waits for inventory confirmation before choosing another ore. Longer walks no longer hit the old short collection timeout. If pickup fails, it pauses at the drop.
- **Direct approach:** it now takes immediate tunnel steps toward debris instead of waiting for a regional route search.
- **Lava plugging:** it places actual plain netherrack, basalt or blackstone from your inventory into encountered lava and waits for the placed block before advancing. Keep a supply of these blocks.
- **Auto totem:** normal paced spare-totem swaps remain active while ON, including while the F7 menu is open.
- **F7 controls:** the new binding works when upgrading from saved F8 settings. Instructions and labels now use F7.

Mending repair, 64-debris ender-chest storage, red highlighting and loaded-player logout remain available. Bring XP bottles, a Mending diamond/netherite pickaxe, spare totems, an ender chest and building blocks. Silk Touch allows chest recovery.

### Validation

Actual local Minecraft survival tests passed for F7, direct mining, real lava plugging, pickup after both self-mined and externally broken debris (including walking six blocks to the drop), server-side XP repair, a real totem pop/refill while the F7 screen remained open, server-confirmed 64-debris ender-chest transfer and loaded-player logout. Unit/contract checks cover direct steps and inventory-confirmed collection across long walks.

ClamAV 1.5.4 scanned the final JAR with zero detections. This is not Microsoft Defender certification. Server-hidden ore/players cannot be revealed; no anti-cheat compatibility or lava-safety guarantee is made. Use automation where permitted. Native tests used an isolated Linux/Mesa local world, with no public server connected to or modified.

- [Source and build instructions](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.0.1-source.zip)
- [SHA-256 checksums](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/SHA256SUMS-netherite-finder-v1-1.0.1.txt)
- [Scan report](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/SCAN-REPORT-netherite-finder-v1-1.0.1.txt)
- [F7 menu preview](https://raw.githubusercontent.com/fragng/astra-client/netherite-finder-downloads/downloads/netherite-finder-v1-1.0.1-menu.png)

# Netherite Finder V1

Minecraft Java **1.21.11**, **Fabric Loader 0.19.3+**, **Java 21**.
Fabric API is included as an unchanged Fabric nested JAR. This is a new
mod, independent of Crystal Client and Astra Client.

## Install and start

Put `netherite-finder-v1-1.0.1.jar` in your Fabric instance's `mods` folder.
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
installable remapped JAR is `build/libs/netherite-finder-v1-1.0.1.jar`.
The source includes route contract tests. The external native test observer
and its local world are excluded from release files.

The bundled Fabric API **0.141.6+1.21.11** is distributed unchanged under
Apache-2.0. Its license is in `META-INF/licenses` inside the JAR and in
`vendor/Fabric-API-LICENSE.txt` in the source. Original project/source:
https://github.com/FabricMC/fabric . No operating-system helpers, browser
engines or executable installers are included.
