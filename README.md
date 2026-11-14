# Astra Client 1.8.2

Cosmetic client mod for Minecraft Java **1.21.11**, **Java 21**, **Fabric Loader 0.19.3+**, and **Fabric API 0.141.6+1.21.11**.

[Download Astra Client 1.8.2.jar](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.8.2.jar)

## Install

Remove previous Astra Client jars from your instance's `mods` folder. Install `astra-client-1.8.2.jar` alongside Fabric API and launch the Fabric profile. Press **Right Shift** in a world to open the client menu; Right Shift, Escape and X close it.

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

On Windows use `gradlew.bat`. Install `build/libs/astra-client-1.8.2.jar`, not the sources jar.

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

The original JAR is unmodified. Its metadata labels the license GNU GPLv3 and its included license file is AGPLv3; both are preserved. `THIRD-PARTY-FREELOOK.txt` inside Astra contains its bundled license and source details. The [complete source archive](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.8.2-source.zip) includes Astra's integration and the matching upstream 1.2.8 source/build scripts under `third-party/freelook/upstream`, pinned to [e9415883](https://github.com/Celibistrial/freelook/tree/e9415883af0fb031a0f3bb49c4e701e9b575bb8f).

**Visuals → Menu Background → Fake Media** remains an optional local-only decoration. In F5 it draws the pink media badge beside your own rendered name. It never changes your server name, rank, team, permissions or network packets, and other players cannot see it. It hides in first person, menus, with F1, and when invisible/spectating. It defaults to Off.

Open/close transitions use quintic easing, subtle zoom and short movement. Rounded panels use cached nine-slice sprites. Smooth animations Off makes transitions immediate. Reset is in Settings and resets the Freelook enable/bind and Fake Media preference too.
