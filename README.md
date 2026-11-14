# Astra Client 1.8.1

Cosmetic client mod for Minecraft Java **1.21.11**, **Java 21**, **Fabric Loader 0.19.3+**, and **Fabric API 0.141.6+1.21.11**.

[Download Astra Client 1.8.1.jar](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.8.1.jar)

## Install

Remove previous Astra Client jars from your instance's `mods` folder. Install `astra-client-1.8.1.jar` alongside Fabric API and launch the Fabric profile. Press **Right Shift** in a world to open the client menu; Right Shift, Escape and X close it.

## Menu categories

- **Visuals:** menu-only brightness, Minecraft FOV, Bubble Font, background themes, Reactive Background and local Fake Media.
- **Settings:** smooth animations, button sounds, and reset Astra preferences.
- **Jamble / Best Buds:** labelled placeholders for future features.
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

On Windows use `gradlew.bat`. Install `build/libs/astra-client-1.8.1.jar`, not the sources jar.

Coiny is bundled under the included `COINY-OFL.txt`. Background artwork is bundled locally; only lyric lookup requires internet. No gameplay cheats are included.

## Validation limits

UI, category navigation, size, themes, previews and lyric transitions were exercised inside Minecraft on Linux using a separate development-only media/lyrics fixture. The fixture and synthetic song are excluded from the mod. The production PowerShell loop and Java media protocol have automated mock tests; connection recovery was exercised with real substitute child processes. Live Windows Spotify playback remains unverified on this Linux host. No hardware FPS improvement is claimed. See `TESTING.md` for checks.

## Menu transitions and Reactive Background (1.8.0)

The Right Shift menu now fades and gently scales/slides when opening and closing. Category changes fade the old page out, then slide/fade the new page in. Rapid category clicks select the latest requested page. X, Escape and Right Shift all use the close transition. Mouse positions use the animated panel transform; moving page controls briefly ignore input until their transition finishes. Elapsed-time transitions finish promptly even when a frame is slow. **Settings → Smooth animations** makes opening, closing and page changes immediate when Off.

**Visuals → Menu Background → Reactive Background** enables the optional moving space scene. Its description is **Makes the Menu Look 100X Better.** The same saved toggle appears beneath the theme buttons in the title screen's **Menu Background** panel. Narrow title windows use slimmer button widths so the new panel does not overlap the main controls; the Mods button keeps its original position. It defaults to Off and loads from `config/astra-client.json`.

When On, the background drifts slowly and cached sprites show meteors, rockets, shooting stars, twinkling stars and passing ringed planets. The scene is restricted to the title screen and Astra menu; it does not draw into gameplay, inventory or chest screens. Normal title mode keeps Minecraft's panorama beneath the optional effects. Turning Smooth animations Off freezes Astra's effects and wallpaper drift. The original Minecraft panorama retains its own vanilla behaviour. Reset turns Reactive Background Off.

The scene has a fixed maximum of 19 sprite submissions per frame and uses Minecraft's GUI atlas, with no particle spawning or per-frame image loading. `tools/generate_space_sprites.py` authors the bundled sprites; Pillow is a development dependency only. The description is cosmetic; no FPS increase is claimed.

## Essentials, Fake Media and softer motion (1.8.0)

**Essentials** replaces General. It integrates the original [FreeLook mod by jmilthedude](https://modrinth.com/mod/freelook-og), version 1.6.0 for Minecraft 1.21.11, bundled under its MIT license. A separate FreeLook installation is unnecessary. Remove an existing standalone copy to avoid duplicate mod IDs. Its source is [FreeLook-MultiLoader](https://github.com/jmilthedude/FreeLook-MultiLoader); redistribution details are in `THIRD-PARTY-FREELOOK.txt` inside the jar and `third-party/freelook/LICENSE.txt` in the source.

Enable **Freelook** and hold your bind (default **Left Alt**) from any camera view. It temporarily enters rear third person, where mouse movement rotates only the camera. Release restores your previous perspective; you no longer need to press F5 manually. If you already use rear third person, the normal smooth camera return is retained. The camera keeps Minecraft's normal third-person collision. It has no detached freecam, world-brightness override, entity detection, reach, movement assistance or automated actions. Opening a menu, disabling Freelook or losing window focus ends the hold and restores the previous view. A manual F5 perspective change during a hold is respected. This describes its behaviour; individual servers decide whether they permit Freelook.

Use **Set a key** and press a keyboard key or mouse button. Escape or Delete clears the binding and shows **Not bound**. Escape is never assigned as an activation key; older saved Escape bindings are migrated to unbound. Escape outside key capture still closes the menu. This supports individual keys/scancodes and mouse buttons that Minecraft receives, rather than OS-reserved shortcuts, hardware-only Fn keys or key combinations. A conflict notice identifies shared native bindings; the real FreeLook mapping is also available in Minecraft Controls. Bindings save in both Astra configuration and native options.

**Visuals → Menu Background → Fake Media** is an optional, local-only decoration. In F5 it draws the reference's pink media badge beside your own rendered name. It never changes your server name, rank, team, permissions or network packets, and other players cannot see it. It hides in first person, menus, with F1, and when invisible/spectating. It defaults to Off.

Open/close transitions use a softer quintic easing curve, less zoom and shorter movement. Rounded client panels now use cached nine-slice sprites rather than repeated scanline rectangles. Smooth animations Off still makes transitions immediate. Reset moved to Settings and resets the Freelook enable/bind and Fake Media preference too.

## Freelook activation fix (1.8.1)

The 1.8.0 gate required manual rear F5 mode. A held bind now enters that camera mode automatically and restores the prior camera view on release or interruption. Essentials describes the new behaviour. Saved/native Escape bindings are treated as unbound, and the key-capture label explicitly explains Escape/Delete clearing.
