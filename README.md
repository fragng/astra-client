# Astra Client 1.24.0

Version 1.17.0 has been withdrawn at the owner's request. The recommended version is 1.24.0.

Cosmetic client mod for Minecraft Java **1.21.11**, **Java 21**, **Fabric Loader 0.19.3+**, and **Fabric API 0.141.6+1.21.11**.

[Download replacement Member edition](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.24.0.jar) · [Download replacement 30-day Premium edition](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.24.0-premium.jar)

**Defender verification is pending.** These replacements retain the script-free native media bridge from 1.14.2 and include source/checksums. A scan with another engine is not proof that Defender will accept a file. Keep any antivirus block in place and report the exact threat name and affected filename if it persists.

[SHA-256 checksums](downloads/SHA256SUMS-1.24.0.txt) · [Security review](SECURITY.md) · [Scan report](downloads/SCAN-REPORT-1.24.0.txt)

## Install

Remove previous Astra Client jars from your instance's `mods` folder. Install **one** edition (`astra-client-1.24.0.jar` or `astra-client-1.24.0-premium.jar`) alongside Fabric API and launch the Fabric profile. Press **Right Shift** in a world to open the client menu; Right Shift, Escape and X close it.

Jamble is back to its original hotbar-only mode. Enable it, then receive a Host item and Viewer item together to show their numbers, icons and winner. The payment queue, J-key review menu, stake limits and payout controls have been removed.

## Menu categories

The sidebar groups appearance controls first, then tools, with Settings and Buy Premium at the bottom:

- **Visuals:** menu brightness, Minecraft FOV, menu themes, Reactive Background, Bubble Font and a Custom Sky preview picker.
- **HUD:** Astra watermark, moon logo and local Fake Media badge.
- **Spotify HUD:** desktop linking, playback, HUD size/themes and HUD lyrics.
- **3D Characters:** six self-only articulated cosmetic models with a SpongeBob icon, 3D previews and exclusive On/Off switches.
- **Essentials:** Freelook and its keyboard/mouse binding, plus a saved Fullbright toggle.
- **Customize Totem — Premium:** the five solid 3D DonutSMP creator totems.
- **Jamble — Premium:** original named-item hotbar tracking, Host/Viewer cards and winner announcements.
- **Settings:** animation, button sounds, Discord Capture Mode and reset preferences.
- **Buy Premium:** Discord-logo button linking to https://discord.gg/gazebo through Minecraft's native link confirmation.

**Active Premium is required for Custom Sky, Lyrics In Sky, Customize Totem and Jamble.** Member mode can browse sky previews and see clearly labelled locked feature pages. Existing selections are retained when Premium is inactive; their effects stop, native totem/sky rendering returns and pending Jamble results clear. Other Astra functions remain available.

## 3D Characters (1.24.0)

Open **Right Shift → 3D Characters** on the **first page**, identified by the SpongeBob face icon. The six choices are **SpongeBob SquarePants, DrDonutt (real-life-inspired), Patrick Star, Squidward Tentacles, Mr. Krabs and Sandy Cheeks**. They are available in both **Member and Premium**.

Each character has its own On/Off switch and a live 3D preview using the same curved model as the game. Turning one On replaces your local player model; the previous character switches Off automatically. Turn the active switch Off to restore your normal player and skin. All switches start Off. The selection saves as `characterStyle` in `config/astra-client.json` and loads at startup. **Reset Astra preferences** also restores the normal player.

Use **F5** to view the model in-game, or open your inventory to see its player preview. Empty-hand first-person rendering uses matching character arms/hands. Native walking, head movement, crouching, using items and attack poses animate the models. Held items stay visible. Character outfits replace the cosmetic armor/cape layers while active; your equipped items, defense, durability and movement keep working normally. Hitboxes and eye height retain their Minecraft values.

Version **1.24.0** adds animated living details: blinking eyelids, subtle breathing, mouth movement timed to the audio’s actual volume pattern, and highlighted 3D sweat beads. Sweat builds during sustained sprinting, burning or low health, follows the curved face, then fades after recovery. **Animated Details** below the character cards can disable these additions. Smooth animations Off or Performance Mode freezes decorative movement. The same details appear on the real F5 model and the native menu previews. Fine clothing seams, fur tufts, shell joints, hair strands, a recessed Patrick belly button and existing facial shading add depth. These remain stylised 3D models, with no claim of photorealism.

Existing surface details remain: SpongeBob has actual shallow, closed pores with solid material behind them, curved cheeks and eye highlights. Subtle cached vertex-colour variation gives skin and clothing softer material detail. All six retain their curved anatomy and smooth shading. These remain stylised 3D cosmetics rather than photorealistic likenesses.

This is a local visual cosmetic: other players keep seeing your normal server-side skin, and other players' models/skins on your screen remain unchanged. Cached articulated geometry and a shared colour atlas are reused between the actual player and native Minecraft skin previews, with independent poses so preview rendering does not disturb world animation. Curved surfaces are built once per character, rather than rebuilt every frame. The sidebar retains the SpongeBob face icon.

The authoring source is `tools/generate_characters.py` (Python standard library only); generated shape definitions and textures are bundled in the mod. No model/skin download or account service is needed at runtime. The first sidebar page has nine sections; the PvP page retains its separate eight categories.

The old header star is replaced with the supplied **moon logo at the top right**, beside the player profile and controls. The profile head and rank remain visible.

## Character voice lines (1.24.0)

Open **3D Characters → Voice Lines**. Choose a character to enable its speech and play its greeting automatically. Use **Preview voice** to audition it again. The pack contains **648 bundled neural speech recordings**: six distinct voices, 27 event types and four variations per event. Two new personality-specific variants per event double the previous line count. Speech uses licensed Piper/VCTK and public-domain LJ Speech models, with brighter SpongeBob, deeper/slower Patrick, nasal Squidward, gravelly Mr. Krabs and brighter American Sandy profiles. DrDonutt uses an original generic voice. These are character-inspired synthetic performances, not official actor recordings or an exact voice-match claim. The model/dataset attribution, source, license and authoring instructions are in [CHARACTER_VOICES.md](CHARACTER_VOICES.md), also bundled with the audio.

Reactions cover totem activation; rain, clear skies, thunder and time of day; damage, healing, death/respawn and a recently attacked mob's death; joining and dimension travel; swimming, Elytra flight and fire; mining/diamonds, food completion, fishing casts, sleep, crafting, containers, experience levels and visible advancements. They react to observed Minecraft state and native events. The feature does not perform gameplay actions or send chat/commands.

Speech starts **On automatically**. Selecting a character enables its voice and plays a greeting; no settings visit is needed. The previous release’s saved Off preference migrates once. A manual Off saved afterward persists on restart; selecting another character enables that character’s voice again. The page offers a saved **volume slider**, **Calm / Normal / Chatty** frequency and five independent groups: Weather and time, Combat and survival, Exploration and travel, Items and activities, Milestones. Important reactions can interrupt a lesser line. Quiet events are discarded during cooldowns, preventing a delayed chatter queue. Turning speech Off, selecting the normal player or disconnecting stops playback. Native Minecraft **Voice/Speech** and master volume also apply. Subtitles show the spoken line when enabled in Minecraft.

All audio plays locally through Minecraft. No speech engine, model download, web account, microphone, helper program or online request is required during play. The characters, audio and Small Totem option are available in both editions; equipping a custom DonutSMP totem still requires active Premium.

## Small Totem (1.24.0)

Open **Customize Totem → Small Totem** at the top of the page or inside the DonutSMP Pack. It works with Minecraft's normal totem and all five custom designs. On reduces totems to **55% in both first-person hands**, preserving their facing direction. Off immediately restores the original size. Inventory/previews, dropped items, third-person items and the totem-pop animation retain their normal size. Other held items and original stack components remain unchanged. The switch is available on the Member page even while the custom pack is locked; it saves across restarts.

## Six menu backgrounds and travel transitions (1.20.0)

Choose **Normal, Galaxy, Nebula, Astra, Sunset or Beachy Sands** in the title screen's right-hand **Menu Background** panel or **Right Shift → Visuals → Menu Background**. Both menus share the same saved choice, available in **Member and Premium**. Sunset has a warm orange/violet mountain-and-water landscape; Beachy Sands has golden sand, turquoise water and palms. Both wallpapers are bundled locally.

Switches blend over **1.35 seconds**: the outgoing scenery travels left while the arriving scene eases in from the right. Buttons and text stay still. Clicking again during travel continues smoothly from the current blend toward the latest choice. Custom backgrounds also drift slowly while idle. Normal retains Minecraft's live title panorama and the client menu's clean navy background.

All six title-screen choices fit with a margin from the screen edge. The client menu uses a **three-column, two-row** selector, with Reactive Background and Bubble Font below it. Very short title screens hide the descriptive sentence below Reactive Background to keep every control accessible.

**Smooth animations Off** or **Performance Mode On** makes changes immediate and freezes decorative custom-background drift. Reactive Background remains separate: travel works with its meteors/planets/rockets Off. Textures are preloaded into Minecraft's resource cache; blending uses fixed-size state and cached textures rather than per-frame image decoding or new offscreen render targets.

The choice saves in `config/astra-client.json`, including `sunset` and `beachy_sands`, and returns after restarting. World sky/dimension and Spotify HUD themes keep their own settings. Original hotbar-only Jamble remains intact, with payment features removed.

## PvP page (1.19.0)

Open **Right Shift → PvP >** in the bottom-right corner. **< Client** returns to your original categories. Both pages keep their selected category while you switch; tab/page transitions use the same smooth animation. The PvP page is available in **both editions**, with eight item-icon categories:

| Category | Working controls |
| --- | --- |
| Crystal PvP | Low Fire, Hide Explosion Particles, Crystal Count, Totem Count |
| Sword PvP | Attack Cooldown, Held Item Durability, Armor Durability, native Hurt Tilt slider |
| Spear + Mace | Fall Distance, Wind Charge Count, Held Item Durability, Active Use Timer |
| Mace | Fall Distance, Wind Charge Count, Attack Cooldown, Armor Durability |
| UHC | Golden Apple Count, Own Effect Timers, Absorption Hearts, Low Fire |
| Axe PvP | Attack Cooldown, Shield Status, Armor Durability, native Hurt Tilt slider |
| Pot / SMP | Ender Pearl Count, Potion Count, Own Effect Timers, Food and Saturation |
| Bow PvP | Arrow Count, Bow Draw, Crossbow Status, Held Item Durability |

Custom toggles start **Off**. Each enabled HUD setting contributes to one compact panel, rather than spawning separate boxes. **Move PvP HUD** releases the cursor so you can drag it clear of Spotify, Jamble and server HUDs; **HUD size** adjusts it from 60–100%. The default position sits lower on the left to clear Spotify on small windows. Positions are screen-relative and clamped on resize. Empty settings show a clearly labelled preview in the editor, without enabling anything in game. F1/debug and open screens hide the gameplay panel.

**Low Fire** lowers the burning overlay in first person, retaining visible flames at the bottom. **Hide Explosion Particles** suppresses both explosion flashes and their emitters, including end-crystal explosions and other explosion particles such as TNT. It does not change explosion damage, sound or world blocks. Other particle types keep their normal behaviour. Already spawned particles finish naturally when the setting changes.

HUD data comes from your own client state. Inventory counters include your offhand once. Golden apples show regular and enchanted counts separately; potions count all bottled, splash and lingering potions, and arrows include tipped/spectral variants. Armor uses H/C/L/B for helmet/chest/legs/boots remaining percentages. The held-item row appears for damageable main-hand items. Shield and crossbow rows appear while equipped; Bow Draw appears while drawing a bow, using Minecraft's actual bow-power calculation. Active Use Timer measures held-item use time, not predicted damage. Own Effect Timers show up to three effects in a stable order. No targeting, attacks, inventory actions, enemy information or packet changes are added.

Controls repeated in several categories **share one saved value**, so Low Fire or Armor does not need enabling twice. Custom switches, HUD size and position save in `config/astra-client.json`; **Hurt Tilt** uses Minecraft's native Damage Tilt setting and options file, staying synchronized with Minecraft's Accessibility settings. Reset Astra preferences clears the custom PvP settings; native Hurt Tilt remains your Minecraft preference. Information is cached once per client tick; rendering does not rescan inventory.

## Custom Sky and Lyrics In Sky

Open **Visuals → Custom Sky / Premium**. Click a thumbnail to choose **Northern Echo's, Galaxy, Nebula, Astra, Solar Dusk or Midnight**. Only one sky is active. The image cards use the same bundled seamless panoramic textures as the actual sky dome; they are not on/off toggles. **Minecraft sky** immediately restores the native sky. The selection saves across restarts.

The custom panorama draws in the normal Overworld sky pass, blends into the native horizon and leaves terrain, fog distance, world lighting, weather, sun, moon, clouds and server time unchanged. Nether and End skies are untouched. The dome's vertex buffer is cached; one draw renders it, and smooth slow rotation freezes when animations or Performance Mode's decorative effects are disabled. Resource reload recreates the cached buffer safely. Lyric glyph geometry is cached in a bounded six-line cache and rebuilt on font/resource changes, rather than rerasterising text every frame. The original panorama-authoring script is `tools/generate_sky_textures.py`; Python/Pillow are not runtime requirements.

**Lyrics In Sky: ON/OFF**, directly below the previews, explicitly enables/disables synchronized Spotify lyrics. They render as a fixed celestial object in the actual sky pass, with soft luminous edges and smooth line fades/scrolling. The default position is South, 40 degrees above the horizon. Turning your view does not drag the lyrics along, and walking does not turn them into a nearby floating label. No HUD panel follows the camera. It works with a custom sky or Minecraft's normal Overworld sky, with the Spotify HUD hidden as well as visible. Enabling it starts the existing desktop link. A Windows 10/11 desktop Spotify session and available timestamped LRCLIB lyrics are required. Missing, instrumental, unsynced or untimed lyrics do not invent words/timing. Line transitions ease using the same lyric-motion logic as the HUD.

**Set Sky Position** captures your current viewing direction once and saves it. Face the part of the sky you want, open the menu and click it. Elevation is limited to 15–75 degrees so the placement stays in the sky. The saved compass direction/elevation persist across restarts; turning lyrics Off immediately hides them and releases their cached glyph meshes.

Sky lyrics render behind terrain, roofs and clouds as part of the sky; solid geometry naturally covers them. They hide with F1, the debug overlay, menus, underwater views, blindness/darkness, unsupported dimensions or inactive Premium. They do not alter server chat, names or other players' view. This is a local visual setting, not a server rank.

Custom preferences save automatically in `config/astra-client.json` and load at startup. FOV uses Minecraft's actual option. Menu brightness leaves world gamma unchanged. Bubble Font switches immediately between Coiny bubble lettering and Minecraft's normal font, including text measurement. Reset keeps Minecraft's FOV, gamma and music volume.

The title screen offers Normal, Galaxy, Nebula, Astra, Sunset and Beachy Sands backgrounds with shared selection and smooth travel transitions; Normal retains Minecraft's panorama. Main title buttons align with Mod Menu. Native Minecraft buttons have rounded styling.

## Discord screen sharing

For a black or frozen Discord stream, enable **Right Shift → Settings → Discord Capture Mode** before starting the stream. It switches Minecraft to a normal window, disables pause on lost focus, and bypasses the native short/long AFK render throttle while retaining your normal FPS cap. The window is named **Astra Client | Minecraft 1.21.11** in this mode; choose it from Discord's **Share Your Screen → Applications** list. Leave the game open rather than minimizing it.

The mode is optional and off by default. Your previous fullscreen/pause preferences are backed up in Astra's config, survive a restart and are restored when the mode is disabled or Astra preferences are reset. Native option changes you deliberately make while it is enabled are preserved when they differ from the applied preset. The original Astra logo remains; the separate Windows process taskbar-ID override from 1.14.2/1.15.0 has been removed as a compatibility precaution.

This addresses application-side fullscreen, pause and AFK-throttling causes; it does not modify Discord, install capture hooks, access your account or bypass Windows protections. Game rendering/focus/restore behaviour is tested in Minecraft on Linux. A live Windows Discord stream and audio capture could not be verified on that host. If the window still captures black, try Discord's full-display sharing, and check that Discord and Minecraft run on the same GPU. Discord capture-method settings and GPU drivers can also affect the result.

## Fullbright

Open **Right Shift → Essentials → Fullbright**, below Freelook. The switch is available in both Member and Premium, is off by default and saves automatically across restarts. Turning it on replaces the client world lightmap with full-bright lighting; Off immediately lets Minecraft rebuild its normal lightmap. Reset Astra preferences also turns it off.

This does not edit Minecraft's gamma/brightness option, Astra's menu brightness, server/world light levels, block data, time or potion effects. Your native brightness setting stays intact while Fullbright is enabled and after it is disabled. The native lightmap update cadence is retained, without a new shader or texture allocation every frame. Shader packs which replace Minecraft's lightmap may handle lighting independently.

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

Windows 10 version 1809 or later / Windows 11 and Spotify's desktop app are required. Version 1.14.2 and later read Windows Global System Media Transport Controls directly through the system WinRT APIs and the JNA libraries already supplied by Minecraft. It does **not** launch PowerShell, compile helper scripts, start an executable, download a native bridge, change execution policy or alter antivirus settings. Metadata and playback commands stay on a single background COM worker; Minecraft's tick/render thread never waits on a media request.

The worker filters for Spotify, reads song/artist/album, supported controls and the Windows timeline. It releases COM interfaces and strings, times out/cancels asynchronous requests, and retries failures after ten seconds. Disable Desktop link to stop it, or use Reconnect. Native failures are logged under **Astra Spotify**. Spotify plays audio through its own app; Minecraft's Music volume is separate. Browser-only Spotify and non-Windows integration remain unsupported.

**Security review:** a friend of the client owner reported a Microsoft Defender threat alert on the previous public download. The exact detection name and affected-file hash were unavailable. The old encoded/hidden PowerShell helper was an unnecessary mechanism and a plausible trigger; this does not establish the actual Defender verdict or prove a false positive. It has been removed completely from the replacement installable JAR. See [SECURITY.md](SECURITY.md) for the review and validation limits. Keep security protection enabled; never add an exclusion or override a block to use Astra.

## Build

Use a Java 21 JDK:

```sh
./gradlew build
./gradlew runClient
```

On Windows use `gradlew.bat`. Install `build/libs/astra-client-1.24.0.jar`, not the sources jar.

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

The original JAR is unmodified. Its metadata labels the license GNU GPLv3 and its included license file is AGPLv3; both are preserved. `THIRD-PARTY-FREELOOK.txt` inside Astra contains its bundled license and source details. The [complete source archive](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.24.0-source.zip) includes Astra's integration and the matching upstream 1.2.8 source/build scripts under `third-party/freelook/upstream`, pinned to [e9415883](https://github.com/Celibistrial/freelook/tree/e9415883af0fb031a0f3bb49c4e701e9b575bb8f).

**Visuals → Menu Background → Fake Media** remains an optional local-only decoration. In F5 it draws the pink media badge beside your own rendered name. It never changes your server name, rank, team, permissions or network packets, and other players cannot see it. It hides in first person, menus, with F1, and when invisible/spectating. It defaults to Off.

Open/close transitions use quintic easing, subtle zoom and short movement. Rounded panels use cached nine-slice sprites. Smooth animations Off makes transitions immediate. Reset is in Settings and resets the Freelook enable/bind and Fake Media preference too.

## Reference icons, Minecraft profile and separate Premium download (1.24.0)

Visuals, Jamble, HUD, Spotify HUD and Essentials use the supplied reference designs as colour icons. Best Buds is replaced by **Customize Totem**, with the vanilla Totem of Undying texture. Settings keeps its gear icon. Icon textures are cached resources; no downloads occur during menu rendering.

The header's top-right portrait uses your current Minecraft skin, including its hat layer. Below it, **Member** is grey and active **Premium** is gold with subtle sparkles. The gear next to X opens **Profile**, with your Minecraft name, head, rank and (in Premium) remaining time and the local expiry date. Turning Smooth animations Off freezes sparkles.

There are two separate downloads. **Choose one; both have the same Fabric mod ID.** Member edition always shows Member. Premium edition starts a **30-day local cosmetic Premium period on its first launch**, persists that start date across restarts in `config/astra-premium.json`, and returns to Member after expiry. Its Profile page shows a live countdown. Expiry does not disable Minecraft or remove the regular client features. Reset Astra preferences does not restart the Premium period.

There is **no Premium server, redemption code, account verification, owner administration or network check**. The implementation and bundled assets match; active Premium enables custom skies, sky lyrics, creator totems and Jamble. The rank is an Astra cosmetic label and never changes DonutSMP server ranks. The local period can be reset by deleting/modifying local data; it is not server-enforced licensing. Dates use the device's local timezone; elapsed-time accounting also avoids extending a running period merely by turning the system clock backwards.

To build the separate edition with Java 21:

```sh
./gradlew build -PpremiumEdition=true
```

This produces `build/libs/astra-client-1.24.0-premium.jar`. Plain `./gradlew build` produces Member edition. The JAR's `astra-edition.json` records the edition; there are no hidden credentials or account endpoints.

## DonutSMP Pack (1.24.0)

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

## Performance Mode for streamers (1.24.0)

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

## Solid 3D creator totems (1.24.0)

All five DonutSMP Pack designs now use **closed 3D cuboid character models**, replacing the old `minecraft:item/generated` sprites. Heads, torsos, arms and separate legs have front, back, side, top and bottom faces. The original reference-based front artwork remains; hair, clothing, skin and footwear patches estimate unseen sides and backs.

Jettism has a raised crown with separate points and blue jewels. Farex has a volumetric top hat and brim. Hoozar0 has a red hood with white trim. Jack has a Santa hat, brim, pompom and cyan hoodie seams. Shoe toes also extend forward where applicable. The models use 8–19 cuboids each and are baked by Minecraft's normal item renderer.

The pack menu now renders the actual 3D models at an angle, rather than a flat texture thumbnail. Preview stacks are cached privately and never enter your inventory. Equipping still affects real totems in hands, inventory, third person, ground/frame contexts and the activation animation. Unequip restores the original model, and saved selections require no migration. Performance Mode and Premium dates are retained.

`tools/generate_totem_models.py` authors the model geometry and UV mappings from the existing texture artwork using Python's standard library. No runtime texture processing or new dependencies are required.

## Original Jamble restored (1.24.0)

Enable **Right Shift → Jamble → Enable Jamble** before receiving items. Name Host items **1.1–9.1** and Viewer items **1–9** in an anvil. Receive exactly one of each together into the **hotbar**, within two seconds. Higher wins; **5.1 beats 5**, so Host wins on matching base numbers.

The original Host/Viewer cards show the received numbers and actual item icons for eight seconds. A small **Host Wins!** or **Viewer Wins!** banner appears near the top for roughly 3.5 seconds. There is no waiting HUD before a complete pair arrives. On wide screens, the cards flank Spotify; on narrower screens, Spotify moves below the roll display while it is visible. F1/debug/menu visibility is respected, and turning Jamble Off clears the result. Jamble remains a Premium feature as before.

No payment is required. Existing inventory, main-inventory/offhand/cursor transfers, slot rearrangements and anvil renaming alone do not count as new acquisitions. Multiple ambiguous arrivals are not guessed. The tracker only observes your own inventory and cannot identify the dispenser or player that supplied an item.

The payment listener, payment queue, J-key review screen/keybinding, chat Review links, stake limits, payout confirmation/records and payment HUD/toast have been removed. Previous payment-limit fields in an old config are ignored and disappear on the next Astra save. Minecraft's J key is available to your other bindings. This release retains the PvP page and the rest of Astra's features.

## Offhand orientation fix (1.13.1, retained in 1.24.0)

The five DonutSMP character totems now use matching authored first-person transforms. Minecraft mirrors the left-hand pose itself, so the face stays turned towards you in either hand, including when Left is your Minecraft main-hand preference. Meshes, textures, size, Equip/Unequip, Jamble and other settings are preserved. Disable competing custom-totem mods/packs when using Astra's selected model.

## Native window and taskbar branding (1.14.2 and later)

The game window is titled **Astra Client** from startup, including title-screen/world/server transitions. The existing gold crescent-moon logo is used for the native window and running-app taskbar icons on Windows and X11. Six icon sizes are generated once at startup using Minecraft's native image resizer; no artwork is downloaded or processed each frame. The per-process taskbar identity override was removed in 1.15.1 for capture compatibility; Windows keeps its normal process grouping. This does not modify the launcher, Java executable, registry or pinned shortcuts. Other window systems retain their native icon handling.
