# Astra Client 1.13.0

Cosmetic client mod for Minecraft Java **1.21.11**, **Java 21**, **Fabric Loader 0.19.3+**, and **Fabric API 0.141.6+1.21.11**.

[Download Member edition](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.13.0.jar) · [Download 30-day Premium edition](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.13.0-premium.jar)

## Install

Remove previous Astra Client jars from your instance's `mods` folder. Install **one** edition (`astra-client-1.13.0.jar` or `astra-client-1.13.0-premium.jar`) alongside Fabric API and launch the Fabric profile. Press **Right Shift** in a world to open the client menu; Right Shift, Escape and X close it.

## Menu categories

- **Visuals:** menu-only brightness, Minecraft FOV, Bubble Font, background themes, Reactive Background and local Fake Media.
- **Settings:** smooth animations, button sounds, and reset Astra preferences.
- **Jamble:** opt-in named-item hotbar tracking, Host/Viewer cards, item icons and a winner announcement.
- **Customize Totem:** replaces Best Buds, with Minecraft's actual Totem of Undying icon and the built-in DonutSMP Pack.
- **HUD:** Astra watermark and moon logo.
- **Spotify HUD:** all Spotify HUD preferences, desktop linking, song status and playback controls.
- **Essentials:** hold-to-use Freelook and a configurable keyboard or mouse bind.

Custom preferences save automatically in `config/astra-client.json` and load at startup. FOV uses Minecraft's actual option. Menu brightness leaves world gamma unchanged. Bubble Font switches immediately between Coiny bubble lettering and Minecraft's normal font, including text measurement. Reset keeps Minecraft's FOV, gamma and music volume.

The title screen retains Normal/Galaxy/Nebula/Astra backgrounds; Normal retains Minecraft's panorama. Main title buttons align with Mod Menu. Native Minecraft buttons have rounded styling.

## Inventory rendering

The standalone Music category and its volume/mute controls have been removed. Spotify controls remain in Spotify HUD. Native Minecraft sound settings are kept.

Rounded inventory slots, slot highlights and default tooltip backgrounds now use cached GUI-atlas sprites. Slots use a single sprite, while expandable panels use stretched nine-slice sprites. This removes thousands of repeated rectangle submissions in populated inventories and chests without changing item or tooltip content. The sprites reload through Minecraft's normal resource system. The optional asset generator is `tools/generate_inventory_sprites.py` (Python with Pillow); it is not a runtime dependency.

## Spotify HUD category

Open Spotify's Windows desktop app and start a song. In **Right Shift → Spotify HUD**:

- **Enable Spotify HUD:** show/hide the top-centre card. Enabling also turns on Desktop link and reconnects if disconnected.
- **Enable Lyrics:** show/hide lyrics below the card.
- **Desktop link:** start/stop the Windows media helper.
- **Reconnect:** restart the media helper manually.
- **Spotify HUD size:** change the whole HUD immediately, from 50% to 100%; default 70%.
- **Previous / Play-pause / Next:** control Spotify's media session. Unsupported actions are disabled.
- **Customise Spotify HUD:** choose Galaxy, Astra, Nebula or Black with an immediate live preview. Only one theme is selected. This preference is separate from the main-menu background and saves across restarts. Black is the default.

Close the client menu to see the HUD in-game. The compact card shows song, artist, elapsed time and progress. **Album artwork and the music icon have been removed**, along with their loading/decoding work. The existing separate Astra watermark retains its optional moon logo. The waiting card stays visible even if Spotify is disconnected; its status explains the connection state. F1/F3 hide the HUD. Narrow-screen layout moves the watermark below the card when needed.

## Lyrics and motion

Lyrics come from **LRCLIB** over HTTPS using song title, artist, album and duration when available. No Spotify login is requested. Lookup happens in a background worker, with a bounded in-memory cache. Disabling lyrics or the Spotify HUD cancels an outstanding lookup and prevents new lookups.

Timestamped lines follow Spotify's playback time. Lines scroll vertically into place with fading and a gradual active-line highlight. Ordinary line changes ease smoothly, while seeking or changing tracks selects the correct line immediately. The animation uses elapsed frame time. **Settings → Smooth animations** disables the transition when Off. Missing lyrics, instrumental tracks, missing timing and network failures have clear status text. Plain lyrics are labelled unsynced and cycle for reading every eight seconds of playback; this is not song synchronization.

## Windows desktop integration

Windows 10/11, Windows PowerShell and desktop media-session access are required. The helper uses Windows Global System Media Transport Controls. Spotify continues playing audio through its own app. Minecraft's Music volume is separate from Spotify transport controls. Browser-only Spotify and non-Windows desktop media integration are unsupported.

The helper retries after failure or a stopped process, with a ten-second delay. Disabling the link cancels startup; stale workers cannot overwrite a new connection. Windows PowerShell startup errors are logged under **Astra Spotify** in Minecraft's `latest.log`. The helper stops when the client closes. Timeline advancement accounts for older Windows timestamps, preventing the former five-second progress freeze.

## Build

Use a Java 21 JDK:

```sh
./gradlew build
./gradlew runClient
```

On Windows use `gradlew.bat`. Install `build/libs/astra-client-1.13.0.jar`, not the sources jar.

Coiny is bundled under the included `COINY-OFL.txt`. Background artwork is bundled locally; only lyric lookup requires internet. No gameplay cheats are included.

## Validation limits

UI, category navigation, size, themes, previews and lyric transitions were exercised inside Minecraft on Linux using a separate development-only media/lyrics fixture. The fixture and synthetic song are excluded from the mod. The production PowerShell loop and Java media protocol have automated mock tests; connection recovery was exercised with real substitute child processes. Live Windows Spotify playback remains unverified on this Linux host. No hardware FPS improvement is claimed. See `TESTING.md` for checks.

## Menu transitions and Reactive Background (1.8.0)

The Right Shift menu now fades and gently scales/slides when opening and closing. Category changes fade the old page out, then slide/fade the new page in. Rapid category clicks select the latest requested page. X, Escape and Right Shift all use the close transition. Mouse positions use the animated panel transform; moving page controls briefly ignore input until their transition finishes. Elapsed-time transitions finish promptly even when a frame is slow. **Settings → Smooth animations** makes opening, closing and page changes immediate when Off.

**Visuals → Menu Background → Reactive Background** enables the optional moving space scene. Its description is **Makes the Menu Look 100X Better.** The same saved toggle appears beneath the theme buttons in the title screen's **Menu Background** panel. Narrow title windows use slimmer button widths so the new panel does not overlap the main controls; the Mods button keeps its original position. It defaults to Off and loads from `config/astra-client.json`.

When On, the background drifts slowly and cached sprites show meteors, rockets, shooting stars, twinkling stars and passing ringed planets. The scene is restricted to the title screen and Astra menu; it does not draw into gameplay, inventory or chest screens. Normal title mode keeps Minecraft's panorama beneath the optional effects. Turning Smooth animations Off freezes Astra's effects and wallpaper drift. The original Minecraft panorama retains its own vanilla behaviour. Reset turns Reactive Background Off.

The scene has a fixed maximum of 19 sprite submissions per frame and uses Minecraft's GUI atlas, with no particle spawning or per-frame image loading. `tools/generate_space_sprites.py` authors the bundled sprites; Pillow is a development dependency only. The description is cosmetic; no FPS increase is claimed.

## Essentials and the supplied Freelook mod (1.8.2)

Astra bundles the exact **Freelook 1.2.8 by Celibistrial** JAR supplied by the user. Its SHA-256 is `fe1a32d9e4b8894122f52985c9d81b5cefa7bb7b67e67d17e8d03c495f8ba1e4`. The previous jmilthedude implementation has been removed. Remove previous Astra jars and separate Freelook copies before installing this version; Freelook is included.

Enable **Essentials → Freelook**, choose **Set a key**, and hold that keyboard key or mouse button in a world. Its default is **Left Alt**. Astra uses the attached mod's actual key mapping and native camera/input logic. From first person, the mod enters its configured perspective; when you release the key it restores your previous view. Existing F5 perspectives follow the mod's native behaviour. **M** opens its original settings page while Astra's Freelook option is enabled. That page can select hold/toggle mode and perspective; Astra's instructions reflect the selected mode.

**Escape or Delete clears the binding** to **Not bound**. Escape is never an activation key. Older saved Escape bindings are also cleared at startup. Escape outside key capture closes Astra normally. Individual keyboard keys/scancodes and mouse buttons received by Minecraft are supported; OS-reserved shortcuts, hardware-only Fn keys and combinations are outside the key picker. Conflicting Minecraft bindings are identified. The same real binding is editable in native Minecraft Controls, and the value is synchronised to Astra's saved configuration.

Astra's enable toggle gates activation. Menus, lost window focus, disabling the setting or clearing the bind stop active Freelook using the supplied mod's own stop method. Its server block list is preserved and respected; Astra displays a notice when that list disables Freelook. It defaults to blocking Hypixel. Astra does not clear that list or override a blocked state. Camera collision and player movement remain native; no detached free camera, movement assistance, reach or automation is added. Each server decides which client mods it permits.

The original JAR is unmodified. Its metadata labels the license GNU GPLv3 and its included license file is AGPLv3; both are preserved. `THIRD-PARTY-FREELOOK.txt` inside Astra contains its bundled license and source details. The [complete source archive](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.13.0-source.zip) includes Astra's integration and the matching upstream 1.2.8 source/build scripts under `third-party/freelook/upstream`, pinned to [e9415883](https://github.com/Celibistrial/freelook/tree/e9415883af0fb031a0f3bb49c4e701e9b575bb8f).

**Visuals → Menu Background → Fake Media** remains an optional local-only decoration. In F5 it draws the pink media badge beside your own rendered name. It never changes your server name, rank, team, permissions or network packets, and other players cannot see it. It hides in first person, menus, with F1, and when invisible/spectating. It defaults to Off.

Open/close transitions use quintic easing, subtle zoom and short movement. Rounded panels use cached nine-slice sprites. Smooth animations Off makes transitions immediate. Reset is in Settings and resets the Freelook enable/bind and Fake Media preference too.

## Reference icons, Minecraft profile and separate Premium download (1.13.0)

Visuals, Jamble, HUD, Spotify HUD and Essentials use the supplied reference designs as colour icons. Best Buds is replaced by **Customize Totem**, with the vanilla Totem of Undying texture. Settings keeps its gear icon. Icon textures are cached resources; no downloads occur during menu rendering.

The header's top-right portrait uses your current Minecraft skin, including its hat layer. Below it, **Member** is grey and active **Premium** is gold with subtle sparkles. The gear next to X opens **Profile**, with your Minecraft name, head, rank and (in Premium) remaining time and the local expiry date. Turning Smooth animations Off freezes sparkles.

There are two separate downloads. **Choose one; both have the same Fabric mod ID.** Member edition always shows Member. Premium edition starts a **30-day local cosmetic Premium period on its first launch**, persists that start date across restarts in `config/astra-premium.json`, and returns to Member after expiry. Its Profile page shows a live countdown. Expiry does not disable Minecraft or remove the regular client features. Reset Astra preferences does not restart the Premium period.

There is **no Premium server, redemption code, account verification, owner administration or network check**. The two editions otherwise have the same features. The rank is an Astra cosmetic label and never changes DonutSMP server ranks. The local period can be reset by deleting/modifying local data; it is not server-enforced licensing. Dates use the device's local timezone; elapsed-time accounting also avoids extending a running period merely by turning the system clock backwards.

To build the separate edition with Java 21:

```sh
./gradlew build -PpremiumEdition=true
```

This produces `build/libs/astra-client-1.13.0-premium.jar`. Plain `./gradlew build` produces Member edition. The JAR's `astra-edition.json` records the edition; there are no hidden credentials or account endpoints.

## DonutSMP Pack (1.13.0)

Open **Right Shift → Customize Totem → DonutSMP Pack → Open Pack**. The built-in pack contains five reference-based pixel-art totem designs:

- Drdonut's Totem
- Jettism's Totem
- Farex's Totem
- Hoozar0's Totem
- Jack's Totem

Each card has a live preview and **Equip** button. The selected card glows and its button changes to **Unequip**. Equipping another design switches to it, so only one design is active. Unequip on the selected card, or **Unequip Totem** on the pack overview, restores the original Minecraft/server-resource-pack model. Back to packs and the category buttons use the existing smooth transitions.

The selection saves in `config/astra-client.json` as `totemStyle` and loads on restart. Reset Astra preferences also unequips it. Invalid saved selections fall back to Minecraft's original model. No separate resource-pack installation or reload is needed when changing designs.

This changes the client appearance of actual Totems of Undying in inventory/hotbar, hands, third person, dropped-item rendering and the totem activation animation. It does not give you a totem, move it to your hand, change item names/components/counts, or change its gameplay effect. Other item types retain their original models. The resolver selects a preloaded model identifier, with no per-frame texture decoding, stack copying or full resource reload on Equip.

The pack is included in both Member and the separate 30-day Premium edition. Premium dates are preserved across this update.

## Performance Mode for streamers (1.13.0)

Open **Right Shift → top-right gear → Performance Mode**. This saved, reversible toggle applies a balanced native video preset:

| Setting | Performance preset |
| --- | --- |
| Render distance | Up to 8 chunks |
| Simulation distance | Up to 5 chunks (singleplayer; multiplayer simulation is server-controlled) |
| Entity distance | Up to 75% |
| Clouds | Off |
| Particles | Decreased; an existing Minimal setting is kept |
| Entity shadows | Off |
| Biome blend radius | Up to 1 |

Settings already below these limits stay lower. Applying the preset can briefly rebuild chunks as Minecraft processes the changed video options. The mode does not repeatedly force native settings each frame; you can still adjust Minecraft Video Settings yourself.

While On, Astra skips the optional reactive meteor/rocket/planet scene, freezes its wallpaper drift and decorative HUD/profile pulses, and skips the GPU background blur behind the Astra menu. Themes, Bubble Font, smooth opening/closing, hover/tab transitions, Spotify/music/lyrics, HUDs, Freelook and all five DonutSMP totems remain available. The Reactive Background preference is kept and resumes when Performance Mode is Off; Visuals labels it as paused while the mode is enabled.

Your previous native values and the applied preset are stored with Astra preferences. **Turning Off restores values that still match the applied preset**, including after a Minecraft restart. Any native setting you deliberately changed while the mode was On is kept. Reset Astra preferences turns the mode Off and performs the same restoration. FOV, gamma, screen resolution, FPS cap, VSync and audio preferences keep their existing values.

This reduces rendering work using Minecraft's normal settings. The FPS result depends on your hardware, world, shaders and recording workload; no fixed gain is promised. Both downloads include Performance Mode, and the Premium period is preserved.

## Solid 3D creator totems (1.13.0)

All five DonutSMP Pack designs now use **closed 3D cuboid character models**, replacing the old `minecraft:item/generated` sprites. Heads, torsos, arms and separate legs have front, back, side, top and bottom faces. The original reference-based front artwork remains; hair, clothing, skin and footwear patches estimate unseen sides and backs.

Jettism has a raised crown with separate points and blue jewels. Farex has a volumetric top hat and brim. Hoozar0 has a red hood with white trim. Jack has a Santa hat, brim, pompom and cyan hoodie seams. Shoe toes also extend forward where applicable. The models use 8–19 cuboids each and are baked by Minecraft's normal item renderer.

The pack menu now renders the actual 3D models at an angle, rather than a flat texture thumbnail. Preview stacks are cached privately and never enter your inventory. Equipping still affects real totems in hands, inventory, third person, ground/frame contexts and the activation animation. Unequip restores the original model, and saved selections require no migration. Performance Mode and Premium dates are retained.

`tools/generate_totem_models.py` authors the model geometry and UV mappings from the existing texture artwork using Python's standard library. No runtime texture processing or new dependencies are required.

## Jamble hotbar rounds (1.13.0)

Open **Right Shift → Jamble → Enable Jamble**. It defaults to Off, saves your choice, and shows instructions on the same page.

1. Name the items in an **anvil before dispensing**.
2. Host names must be **1.1 through 9.1**, ending in exactly **.1**.
3. Viewer names must be the whole numbers **1 through 9**, with no decimal.
4. Dispense **one Host item and one Viewer item together into your hotbar**. Main inventory, armour, cursor and offhand slots are not eligible receipt slots.

The higher numeric value wins. The comparison uses integer tenths: Host **5.1** beats Viewer **5**, while Viewer **6** beats Host **5.1**. It shows **Host Wins!** or **Viewer Wins!** in the middle for about 3.5 seconds. Host and Viewer cards appear at the top-middle left/right for 8 seconds, with each item's number and its actual Minecraft item icon below. The most recent completed round replaces the previous result.

Both eligible arrivals must occur within a **two-second window**, allowing slightly separated inventory packets for a simultaneous dispense. More than one new item for the same side in that window is ambiguous, so no winner is guessed. Values 0/10, leading-zero names, other decimals and unnamed items are ignored. Component formatting such as colours is accepted; the underlying name must match a valid number. Items already carried when you enable Jamble or join a world are baselined, not scored; there is a one-second inventory synchronisation period after arming/rejoining.

Tracking compares new hotbar counts against total owned counts. Moving the same items between hotbar slots, from the main inventory or from the offhand/cursor does not create a fresh round. Renaming alone does not create a new physical item gain, and anvil-screen changes are baselined. This is a local read-only receipt overlay: it does not verify a dispenser block's identity, generate rolls, dispense items, change item names/counts or send gameplay actions. The custom-name and new-arrival checks determine the result.

Spotify stays between the two cards when there is room. Compact windows move it below the cards, and the watermark moves out of the way or is temporarily hidden if there is insufficient height above the hotbar. Media playback and saved HUD preferences remain unchanged. The centre announcement draws above other HUDs like a temporary title. F1 and the debug overlay hide Astra HUDs; disabling Jamble immediately clears its cards and pending pair.

Jamble works in both editions and with Performance Mode, Bubble Font and the custom 3D totems. Item stacks are copied only when an eligible result arrives; the opt-in tracker reads inventory once per client tick and does no per-frame network requests or texture decoding.
