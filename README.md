# Astra Client 1.14.2

Cosmetic client mod for Minecraft Java **1.21.11**, **Java 21**, **Fabric Loader 0.19.3+**, and **Fabric API 0.141.6+1.21.11**.

[Download replacement Member edition](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.14.2.jar) · [Download replacement 30-day Premium edition](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.14.2-premium.jar)

**Defender verification is pending.** These replacements remove the retired scripting helper and include source/checksums. A scan with another engine is not proof that Defender will accept a file. Keep any antivirus block in place and report the exact threat name and affected filename if it persists.

[SHA-256 checksums](downloads/SHA256SUMS-1.14.2.txt) · [Security review](SECURITY.md) · [Scan report](downloads/SCAN-REPORT-1.14.2.txt)

## Install

Remove previous Astra Client jars from your instance's `mods` folder. Install **one** edition (`astra-client-1.14.2.jar` or `astra-client-1.14.2-premium.jar`) alongside Fabric API and launch the Fabric profile. Press **Right Shift** in a world to open the client menu; Right Shift, Escape and X close it.

## Menu categories

The sidebar groups appearance controls first, then tools, with Settings and Buy Premium at the bottom:

- **Visuals:** menu brightness, Minecraft FOV, menu themes, Reactive Background, Bubble Font and a Custom Sky preview picker.
- **HUD:** Astra watermark, moon logo and local Fake Media badge.
- **Spotify HUD:** desktop linking, playback, HUD size/themes and HUD lyrics.
- **Essentials:** Freelook and its keyboard/mouse binding.
- **Customize Totem — Premium:** the five solid 3D DonutSMP creator totems.
- **Jamble — Premium:** opt-in named-item hotbar tracking and winner announcements.
- **Settings:** animation, button sounds and reset preferences.
- **Buy Premium:** Discord-logo button linking to https://discord.gg/gazebo through Minecraft's native link confirmation.

**Active Premium is required for Custom Sky, Lyrics In Sky, Customize Totem and Jamble.** Member mode can browse sky previews and see clearly labelled locked feature pages. Existing selections are retained when Premium is inactive; their effects stop, native totem/sky rendering returns and pending Jamble results clear. Other Astra functions remain available.

## Custom Sky and Lyrics In Sky

Open **Visuals → Custom Sky / Premium**. Click a thumbnail to choose **Northern Echo's, Galaxy, Nebula, Astra, Solar Dusk or Midnight**. Only one sky is active. The image cards use the same bundled seamless panoramic textures as the actual sky dome; they are not on/off toggles. **Minecraft sky** immediately restores the native sky. The selection saves across restarts.

The custom panorama draws in the normal Overworld sky pass, blends into the native horizon and leaves terrain, fog distance, world lighting, weather, sun, moon, clouds and server time unchanged. Nether and End skies are untouched. The dome's vertex buffer is cached; one draw renders it, and smooth slow rotation freezes when animations or Performance Mode's decorative effects are disabled. Resource reload recreates the cached buffer safely. The original panorama-authoring script is `tools/generate_sky_textures.py`; Python/Pillow are not runtime requirements.

**Lyrics In Sky**, directly below the previews, places synchronized Spotify lyrics in world space above the horizon. Look upwards in your current viewing direction to see them. It works with a custom sky or Minecraft's normal Overworld sky, with the Spotify HUD hidden as well as visible. Enabling it starts the existing desktop link. A Windows 10/11 desktop Spotify session and available timestamped LRCLIB lyrics are required. Missing, instrumental, unsynced or untimed lyrics do not invent words/timing. Line transitions ease using the same lyric-motion logic as the HUD.

Sky lyrics use normal depth testing: terrain/roofs can block the text. They hide with F1, the debug overlay, menus, underwater views, blindness/darkness, unsupported dimensions or inactive Premium. They do not alter server chat, names or other players' view. This is a local visual setting, not a server rank.

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

Lyrics come from **LRCLIB** over HTTPS using song title, artist, album and duration when available. No Spotify login is requested. Lookup happens in a background worker, with a bounded in-memory cache. Lookup stops when both HUD lyrics and Premium sky lyrics are disabled; either display can use the shared cached lyrics independently.

Timestamped lines follow Spotify's playback time. Lines scroll vertically into place with fading and a gradual active-line highlight. Ordinary line changes ease smoothly, while seeking or changing tracks selects the correct line immediately. The animation uses elapsed frame time. **Settings → Smooth animations** disables the transition when Off. Missing lyrics, instrumental tracks, missing timing and network failures have clear status text. Plain lyrics are labelled unsynced and cycle for reading every eight seconds of playback; this is not song synchronization.

## Windows desktop integration

Windows 10 version 1809 or later / Windows 11 and Spotify's desktop app are required. Version 1.14.2 reads Windows Global System Media Transport Controls directly through the system WinRT APIs and the JNA libraries already supplied by Minecraft. It does **not** launch PowerShell, compile helper scripts, start an executable, download a native bridge, change execution policy or alter antivirus settings. Metadata and playback commands stay on a single background COM worker; Minecraft's tick/render thread never waits on a media request.

The worker filters for Spotify, reads song/artist/album, supported controls and the Windows timeline. It releases COM interfaces and strings, times out/cancels asynchronous requests, and retries failures after ten seconds. Disable Desktop link to stop it, or use Reconnect. Native failures are logged under **Astra Spotify**. Spotify plays audio through its own app; Minecraft's Music volume is separate. Browser-only Spotify and non-Windows integration remain unsupported.

**Security review:** a friend of the client owner reported a Microsoft Defender threat alert on the previous public download. The exact detection name and affected-file hash were unavailable. The old encoded/hidden PowerShell helper was an unnecessary mechanism and a plausible trigger; this does not establish the actual Defender verdict or prove a false positive. It has been removed completely from the replacement installable JAR. See [SECURITY.md](SECURITY.md) for the review and validation limits. Keep security protection enabled; never add an exclusion or override a block to use Astra.

## Build

Use a Java 21 JDK:

```sh
./gradlew build
./gradlew runClient
```

On Windows use `gradlew.bat`. Install `build/libs/astra-client-1.14.2.jar`, not the sources jar.

Coiny is bundled under the included `COINY-OFL.txt`. Background artwork is bundled locally; only lyric lookup requires internet. The installable JAR contains no bundled PowerShell/batch/shell scripts or EXE/DLL helpers. No gameplay cheats are included.

## Validation limits

UI, category navigation, size, themes, previews and lyric transitions were exercised inside Minecraft on Linux using a separate development-only media/lyrics fixture. The fixture and synthetic song are excluded from the mod. The replacement native WinRT bridge has repeatable COM-vtable tests (`./gradlew testWindowsMediaAbi`, also part of `check`). The retired PowerShell bridge/process tests no longer validate the current implementation. Live Windows Spotify playback remains unverified on this Linux host. No hardware FPS improvement is claimed. See `TESTING.md` for checks.

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

The original JAR is unmodified. Its metadata labels the license GNU GPLv3 and its included license file is AGPLv3; both are preserved. `THIRD-PARTY-FREELOOK.txt` inside Astra contains its bundled license and source details. The [complete source archive](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.14.2-source.zip) includes Astra's integration and the matching upstream 1.2.8 source/build scripts under `third-party/freelook/upstream`, pinned to [e9415883](https://github.com/Celibistrial/freelook/tree/e9415883af0fb031a0f3bb49c4e701e9b575bb8f).

**Visuals → Menu Background → Fake Media** remains an optional local-only decoration. In F5 it draws the pink media badge beside your own rendered name. It never changes your server name, rank, team, permissions or network packets, and other players cannot see it. It hides in first person, menus, with F1, and when invisible/spectating. It defaults to Off.

Open/close transitions use quintic easing, subtle zoom and short movement. Rounded panels use cached nine-slice sprites. Smooth animations Off makes transitions immediate. Reset is in Settings and resets the Freelook enable/bind and Fake Media preference too.

## Reference icons, Minecraft profile and separate Premium download (1.14.2)

Visuals, Jamble, HUD, Spotify HUD and Essentials use the supplied reference designs as colour icons. Best Buds is replaced by **Customize Totem**, with the vanilla Totem of Undying texture. Settings keeps its gear icon. Icon textures are cached resources; no downloads occur during menu rendering.

The header's top-right portrait uses your current Minecraft skin, including its hat layer. Below it, **Member** is grey and active **Premium** is gold with subtle sparkles. The gear next to X opens **Profile**, with your Minecraft name, head, rank and (in Premium) remaining time and the local expiry date. Turning Smooth animations Off freezes sparkles.

There are two separate downloads. **Choose one; both have the same Fabric mod ID.** Member edition always shows Member. Premium edition starts a **30-day local cosmetic Premium period on its first launch**, persists that start date across restarts in `config/astra-premium.json`, and returns to Member after expiry. Its Profile page shows a live countdown. Expiry does not disable Minecraft or remove the regular client features. Reset Astra preferences does not restart the Premium period.

There is **no Premium server, redemption code, account verification, owner administration or network check**. The implementation and bundled assets match; active Premium enables custom skies, sky lyrics, creator totems and Jamble. The rank is an Astra cosmetic label and never changes DonutSMP server ranks. The local period can be reset by deleting/modifying local data; it is not server-enforced licensing. Dates use the device's local timezone; elapsed-time accounting also avoids extending a running period merely by turning the system clock backwards.

To build the separate edition with Java 21:

```sh
./gradlew build -PpremiumEdition=true
```

This produces `build/libs/astra-client-1.14.2-premium.jar`. Plain `./gradlew build` produces Member edition. The JAR's `astra-edition.json` records the edition; there are no hidden credentials or account endpoints.

## DonutSMP Pack (1.14.2)

Open **Right Shift → Customize Totem → DonutSMP Pack → Open Pack**. The built-in pack contains five reference-based pixel-art totem designs:

- Drdonut's Totem
- Jettism's Totem
- Farex's Totem
- Hoozar0's Totem
- Jack's Totem

Each card has a live preview and **Equip** button. The selected card glows and its button changes to **Unequip**. Equipping another design switches to it, so only one design is active. Unequip on the selected card, or **Unequip Totem** on the pack overview, restores the original Minecraft/server-resource-pack model. Back to packs and the category buttons use the existing smooth transitions.

The selection saves in `config/astra-client.json` as `totemStyle` and loads on restart. Reset Astra preferences also unequips it. Invalid saved selections fall back to Minecraft's original model. No separate resource-pack installation or reload is needed when changing designs.

This changes the client appearance of actual Totems of Undying in inventory/hotbar, hands, third person, dropped-item rendering and the totem activation animation. It does not give you a totem, move it to your hand, change item names/components/counts, or change its gameplay effect. Other item types retain their original models. The resolver selects a preloaded model identifier, with no per-frame texture decoding, stack copying or full resource reload on Equip.

The pack can be previewed in Member mode; equipping it requires active Premium. Premium dates are preserved across this update.

## Performance Mode for streamers (1.14.2)

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

## Solid 3D creator totems (1.14.2)

All five DonutSMP Pack designs now use **closed 3D cuboid character models**, replacing the old `minecraft:item/generated` sprites. Heads, torsos, arms and separate legs have front, back, side, top and bottom faces. The original reference-based front artwork remains; hair, clothing, skin and footwear patches estimate unseen sides and backs.

Jettism has a raised crown with separate points and blue jewels. Farex has a volumetric top hat and brim. Hoozar0 has a red hood with white trim. Jack has a Santa hat, brim, pompom and cyan hoodie seams. Shoe toes also extend forward where applicable. The models use 8–19 cuboids each and are baked by Minecraft's normal item renderer.

The pack menu now renders the actual 3D models at an angle, rather than a flat texture thumbnail. Preview stacks are cached privately and never enter your inventory. Equipping still affects real totems in hands, inventory, third person, ground/frame contexts and the activation animation. Unequip restores the original model, and saved selections require no migration. Performance Mode and Premium dates are retained.

`tools/generate_totem_models.py` authors the model geometry and UV mappings from the existing texture artwork using Python's standard library. No runtime texture processing or new dependencies are required.

## Jamble hotbar rounds (1.14.2)

Open **Right Shift → Jamble → Enable Jamble**. It defaults to Off, saves your choice, and shows instructions on the same page.

1. Name the items in an **anvil before dispensing**.
2. Host names must be **1.1 through 9.1**, ending in exactly **.1**.
3. Viewer names must be the whole numbers **1 through 9**, with no decimal.
4. Dispense **one Host item and one Viewer item together into your hotbar**. Main inventory, armour, cursor and offhand slots are not eligible receipt slots.

The higher numeric value wins. The comparison uses integer tenths: Host **5.1** beats Viewer **5**, while Viewer **6** beats Host **5.1**. It shows **Host Wins!** or **Viewer Wins!** in the middle for about 3.5 seconds. Host and Viewer cards appear at the top-middle left/right for 8 seconds, with each item's number and its actual Minecraft item icon below. The most recent completed round replaces the previous result.

Both eligible arrivals must occur within a **two-second window**, allowing slightly separated inventory packets for a simultaneous dispense. More than one new item for the same side in that window is ambiguous, so no winner is guessed. Values 0/10, leading-zero names, other decimals and unnamed items are ignored. Component formatting such as colours is accepted; the underlying name must match a valid number. Items already carried when you enable Jamble or join a world are baselined, not scored; there is a one-second inventory synchronisation period after arming/rejoining.

Tracking compares new hotbar counts against total owned counts. Moving the same items between hotbar slots, from the main inventory or from the offhand/cursor does not create a fresh round. Renaming alone does not create a new physical item gain, and anvil-screen changes are baselined. This is a local read-only receipt overlay: it does not verify a dispenser block's identity, generate rolls, dispense items, change item names/counts or send gameplay actions. The custom-name and new-arrival checks determine the result.

Spotify stays between the two cards when there is room. Compact windows move it below the cards, and the watermark moves out of the way or is temporarily hidden if there is insufficient height above the hotbar. Media playback and saved HUD preferences remain unchanged. The centre announcement draws above other HUDs like a temporary title. F1 and the debug overlay hide Astra HUDs; disabling Jamble immediately clears its cards and pending pair.

Jamble requires active Premium and works with Performance Mode, Bubble Font and the custom 3D totems. Item stacks are copied only when an eligible result arrives; the opt-in tracker reads inventory once per client tick and does no per-frame network requests or texture decoding.

## Offhand orientation fix (1.13.1, retained in 1.14.2)

The five DonutSMP character totems now use matching authored first-person transforms. Minecraft mirrors the left-hand pose itself, so the face stays turned towards you in either hand, including when Left is your Minecraft main-hand preference. Meshes, textures, size, Equip/Unequip, Jamble and other settings are preserved. Disable competing custom-totem mods/packs when using Astra's selected model.

## Native window and taskbar branding (1.14.2)

The game window is titled **Astra Client** from startup, including title-screen/world/server transitions. The existing gold crescent-moon logo is used for the native window and running-app taskbar icons on Windows and X11. Six icon sizes are generated once at startup using Minecraft's native image resizer; no artwork is downloaded or processed each frame. Windows uses the per-process app identity `AstraClient.Client` so the running client can have its own taskbar group. This does not modify the launcher, Java executable, registry or pinned shortcuts. Other window systems retain their native icon handling.
