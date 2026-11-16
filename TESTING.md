# Astra Client 1.14.2 validation

- Built with Java 21 for Minecraft 1.21.11 / Fabric Loader 0.19.3.
- Removed the standalone Music category, its music-volume and mute controls, and the unused restoreMusic preference. Native Minecraft sound settings are untouched.
- Opened the real Minecraft client with a separate development-only chest fixture containing 54 named items and multiline lore (90 rendered slots including player inventory).
- Measured the same chest before/after the rendering change, hovering one item and sweeping across all 54 items. The test fixture counted GuiRenderState.submitGuiElement submissions per frame; these are GUI elements, not GPU draw calls or a universal FPS measurement.

| Scenario | Before elements/frame | After elements/frame |
| --- | ---: | ---: |
| Pointer outside slots | 8651 | 868 |
| Hover one item | 8810 | 881 |
| Sweep across items | 8810 | 881 |

The hover scenario submitted 90% fewer GUI elements. This is a diagnostic measurement from a software-rendered Linux development environment, not a hardware FPS guarantee. Item/tooltip content, styles and rounded corners were visually compared.

- Checked cached sprites after F3+T resource reload. No missing sprites or metadata errors appeared, and the tooltip remained opaque over items.
- Navigated all seven remaining categories, including Spotify HUD and General. Verified the existing Spotify HUD theme preference remains saved.
- The atlas sprites use fixed/stretch and stretched-nine-slice scaling; stretch_inner is explicitly enabled to avoid tiling the small panel centre into many quads.
- The optional Python/Pillow asset generator is included; Pillow is not a Minecraft runtime dependency.

The chest fixture and performance instrumentation are outside the project and excluded from the jar/source archive. Spotify playback and lyric handling are unchanged; live Windows Spotify remains unverified from this Linux host.

## Menu transitions and reactive scene (1.7.0)

- Built on Java 21 and exercised the title screen and a real singleplayer world with Mod Menu installed, without a media/performance fixture.
- Verified the title Reactive Background toggle saves and causes visible scene/background movement; the world-menu toggle reads the same saved preference.
- Checked the exact requested description and controls fit below Menu Background on Visuals.
- Exercised all seven categories, Spotify customisation, FOV input and the shared reactive toggle after page transitions.
- Checked open/close paths through Right Shift, Escape and X. Captured transition frames and rapid category retargeting; verified the final page remains usable.
- Disabled Smooth animations and compared static Astra background captures: no movement. Closing/reopening and category changes are immediate with the preference Off.
- Menu tween tests covered elapsed time, smooth midpoint, reversals, settling without overshoot, reduced motion, frame-rate independence and a long frame spanning the page-swap boundary.
- Rechecked rapid page retargeting after the long-frame fix by toggling a control on the final HUD page; it remained interactive.
- Checked Normal title mode with the optional reactive overlay and a 640×480 title window. Main controls and the new panel no longer overlap, and the compact title toggle saves correctly.

Inventory caching from 1.6.1 is preserved. Live Windows Spotify remains unverified; that bridge is unchanged in this release.

## Essentials, badge and motion (1.8.0)

- Java 21 clean build for Minecraft 1.21.11 and Fabric Loader 0.19.3, with the original MIT FreeLook 1.6.0 nested dependency.
- Opened a real singleplayer world with Mod Menu, loaded saved preferences, and navigated the renamed Essentials page. No client/mixin or atlas loading errors appeared.
- Captured Fake Media beside the local player's name in both rear and front F5 views. First person hides it. It changes only the local render state's text and attachment, never the entity's name/team or network state.
- Exercised Freelook enable, keyboard binding (B), Escape cancellation, Delete unbinding, middle-mouse binding, rebind and saved configuration/native options. No crash opening Right Shift.
- A separate development-only observer recorded real player and camera state while synthesizing key/mouse input. In rear F5 view, held B moved the camera from yaw/pitch 0/0 to 100/90 while the player's yaw/pitch remained 0/0 and position remained (8.3740336928, 70, 10.9076492264). Release restored camera 0/0. Camera distance stayed approximately 4 blocks in open space. First-person input retained the native camera/player relationship.
- Upstream FreeLook supports rear third person; front-facing third person is gated off as well as first person. The integration clears upstream state on menus, disabled preference, lost focus or unsupported perspective. Native Camera placement/collision code is retained; no detached/free camera is implemented.
- Re-ran MenuTween elapsed-time, no-overshoot, reversal, settling, reduced-motion and frame-rate-independence checks after changing to quintic easing.
- Verified the new rounded-mask atlas assets render in Minecraft and compacted Visuals controls to keep Fake Media within the background card. Inventory slot/tooltip atlas rendering from the previous release is retained.

The input/state observer is outside the project and excluded from the distributed files. These checks establish the implemented camera behaviour, not server approval or a hardware FPS claim. Live Windows Spotify is unchanged and remains unverified on this Linux host.

Final runtime checks also passed fresh camera-state activation after opening/closing the menu, disabling Freelook while testing mouse input, Fake Media on/off and F1 visibility, reset-to-defaults, and the 640×480 client layout. The final nested-jar hash matches the original FreeLook artifact exactly; both MIT notice and badge/round-mask assets are present.

## Freelook activation and Escape clearing (1.8.1)

- Built the 1.8.1 release jar with Java 21. Ran that packaged, remapped jar with Fabric Loader 0.19.3, Fabric API and its actual nested FreeLook dependency using Loom's production client runner. A separately remapped observation fixture was loaded only for testing; it is excluded from the release and source archive.
- Held a real keyboard bind from FIRST_PERSON, THIRD_PERSON_BACK and THIRD_PERSON_FRONT. All entered rear third-person Freelook and returned to the exact prior perspective after release. Camera yaw changed by 100 degrees under the upstream clamp while player yaw, pitch and position stayed constant. Native camera collision/placement remains intact.
- Repeated activation with a middle-mouse bind. Confirmed disabled Freelook and an unbound mapping cannot activate it.
- Opened the client menu during a held bind and verified perspective restoration. Loss of window focus also restored the prior view. Manual F5 changes during a hold were respected on release.
- Bound B, reopened key capture and pressed Escape. Verified the menu stayed open, the label became `Set a key: Not bound`, custom configuration saved `key.keyboard.unknown`, and B no longer activated Freelook. Escape outside capture still closes the client menu.
- Rechecked the Essentials layout and updated instructions in the actual production client. No mod/mixin errors occurred.

- Restarted the production jar with Escape deliberately saved in both Astra JSON and Minecraft Controls. Startup migrated both files to the native unknown key; Essentials displayed `Not bound`, remained usable, and Freelook stayed inactive.

## Supplied Celibistrial Freelook replacement (1.8.2)

- Removed the jmilthedude FreeLook dependency and all net.ninjadev integration code. Built against and nested the exact user-uploaded `freelook-1.2.8 (1).jar`, SHA-256 `fe1a32d9e4b8894122f52985c9d81b5cefa7bb7b67e67d17e8d03c495f8ba1e4`. Only this Freelook JAR is nested in the release.
- Kept its camera and entity-turn mixins unchanged. Astra accesses its real registered activation key and uses its native stop method for menu/focus/disabled/unbound guards. The native server block list and blocked flag are respected; no blocked-state override was introduced.
- Built on Java 21 and launched the packaged, remapped 1.8.2 JAR in the production Minecraft 1.21.11 / Fabric Loader 0.19.3 runner with Fabric API. Confirmed the nested mod loads as Freelook 1.2.8, with no previous Freelook implementation.
- Tested saved Astra binding B against a deliberately conflicting saved native default Left Alt: the final native activation mapping was B after startup. Initialization runs after the supplied mod registers its mappings and again after Minecraft finishes loading its options.
- Exercised first-person, rear F5 and front F5 holds. Camera yaw moved while player yaw/pitch and position stayed constant. Release restored each original perspective and facing. The uploaded mod retains its native F5 perspective behaviour. Rear camera distance remained about 4 blocks; terrain shortened the front-view camera distance to about 1.5 blocks through normal collision handling.
- Repeated activation with a middle-mouse binding. Verified enable/disable, active menu interruption, loss of window focus, clearing to unbound, Escape keeping the picker screen open while clearing, and Escape outside capture closing Astra normally.
- Exercised the mod's blocked state during an active hold: native Freelook stopped, the previous perspective returned, further presses stayed inactive, and Essentials displayed the blocked-server notice. Unblocking the development fixture restored normal behaviour. This simulates the upstream runtime flag; the actual server list was never cleared or modified.
- Exercised native toggle mode and opened the supplied mod's actual Freelook settings page with M. The native mode/perspective/server controls remain provided by that mod.
- Retained the original JAR metadata/license verbatim. Included the matching upstream 1.2.8 source and build scripts at commit e9415883af0fb031a0f3bb49c4e701e9b575bb8f in the complete source archive, alongside Astra's integration.

The separately remapped state observer and synthetic-input helpers are excluded from both distributable archives. Runtime checks were performed on the Linux test host; live Windows Spotify remains unchanged and unverified here. Server approval and hardware FPS are not claimed.

## Reference icons, profile and separate editions (1.9.0)

- Built Member and Premium production JARs for Java 21 / Minecraft 1.21.11 / Fabric Loader 0.19.3. Their embedded edition descriptors are respectively `premium:false` and `premium:true`; both have the same 30-day duration and include the exact supplied Freelook 1.2.8 dependency.
- Loaded the packaged Member JAR in a real production Minecraft instance. Opened Right Shift, navigated Customize Totem and Profile, and inspected the replacement reference icons, native Totem of Undying texture, Minecraft skin portrait and gray Member label. No Premium timing file was created by Member edition.
- Loaded the separate packaged Premium JAR. Verified `expiresAt - startedAt` is exactly 30 days and the remaining seconds decrease in real time. Inspected the gold Premium label, header sparkles and profile expiry/countdown in the real client.
- The gear opens Profile and all regular category navigation remains available. Best Buds is replaced by Customize Totem. That page explicitly labels future customisation rather than presenting nonfunctional controls.
- Removed the proposed redeem-code, account and owner-management implementation before shipping. No Premium service URL, bearer token, authentication request, redemption control or backend is included. The standalone service draft was discarded and never published or deployed.
- Icon resources and Premium timing checks use cached images and local arithmetic. The six sparkle rectangles are bounded, and preferences still disable animation. Premium dates save at startup/shutdown and once per minute, rather than each frame.

The local cosmetic period is deliberately not server-enforced and can be reset by modifying local files. The rank does not change DonutSMP ranks. No Premium gameplay features are introduced.

- Restarted the packaged Premium JAR and verified the persisted start and expiry timestamps were unchanged. Advanced its local test period to 31 days old through an excluded development observer: the live header and Profile immediately switched to Member, the countdown stopped at zero, and the regular client menu remained available. No renewal period was created.

## DonutSMP totem pack (1.10.0)

- Built Java 21 Member and Premium JARs for Minecraft 1.21.11 / Fabric Loader 0.19.3. Bundled five reference-based 64×64 RGBA sprites, corresponding item models and modern client item definitions.
- Loaded the packaged Member JAR in a real production client. Opened Customize Totem → DonutSMP Pack, equipped all five creators, and checked saved configuration values. Each selected card changed from Equip to Unequip and the previous selection cleared.
- Used a separate development-only observer to call Minecraft's actual ItemModelResolver for each selection across all ten ItemDisplayContexts. Particle sprite identifiers matched each selected custom texture; Unequip resolved the native Minecraft totem sprite in all ten contexts. The observation exercises the real production mixin and baked resource models, rather than just the helper's identifier return value.
- After each probe, asserted the original item stack, count, name, component values and glint override were unchanged. A diamond item continued to resolve its native diamond model. Production code never copies/modifies the stack or sends inventory commands.
- Visually checked Jack's design in both first-person hands, inventory/hotbar, and the Hoozar0 design in the native totem activation display. Used real totems in the singleplayer test world, supplied only by the excluded test fixture.
- Exercised selected-card Unequip, overview Unequip, Back navigation, switching selections and reset-to-defaults. Native rendering returned immediately after Unequip.
- Reloaded resources with F3+T while equipped and repeated native model probes. The custom models remained available with no missing-model/texture errors.

The synthetic-input observer and test commands are outside the project and excluded from distributables. This is a client appearance choice; it does not grant/equip an actual item or change totem mechanics. No hardware FPS claim is made.

- Restarted with the packaged Premium JAR and confirmed Hoozar0 remained equipped and resolved to its custom baked texture. Premium start/expiry timestamps were unchanged. Inspected the pack at 640×480 and exercised the second-row Jack Equip/Unequip hit targets successfully. Both editions contain byte-identical implementation classes.

## Performance Mode (1.11.0)

- Built with Java 21 and launched the actual packaged Member JAR using the production Minecraft 1.21.11 / Fabric Loader 0.19.3 runner.
- Opened the top-right gear and exercised the Performance Mode toggle. Inspected Profile layout, selected state, unblurred in-game background, and the paused-reactive-effects message in Visuals.
- Recorded native Minecraft option values through a development-only observer. The preset changed render distance 10→8, simulation distance 8→5, entity distance 100%→75%, clouds Fancy→Off, particles All→Decreased, entity shadows On→Off and biome blend radius 2→1. Native server logs confirmed singleplayer view/simulation-distance updates.
- Turning Off restored all seven original values. A second baseline with render distance 4, simulation 5, entity range 50%, clouds Off, particles Minimal, shadows Off and blend 0 remained unchanged when enabled; the mode never increased those lower settings.
- Deliberately edited render distance to 6 while On. Turning Off kept that edit while restoring the other untouched preset values. Saved an enabled mode, its original/applied backup, and a deliberate override for the restart check.
- Verified FOV, world gamma, FPS cap, HUD visibility, Spotify HUD, animation preference and equipped Hoozar0 totem selection stayed unchanged. Reactive Background's saved preference remained On while its actual render gate returned false in Performance Mode, then resumed on disabling it.
- The implementation skips Astra menu background blur and its optional reactive scene and drift. It keeps smooth interactions, media/lyrics and totem models. Native option changes occur on toggling, not continuously every frame.

The test observer is excluded from distributables. No hardware FPS gain is claimed from this software-rendered Linux test environment; performance depends on the scene, hardware, shaders and recording workload.

- Restarted with the packaged Premium JAR. The enabled mode, original-value backup and deliberate render-distance override all survived; switching Off restored the other original settings. Reset Astra preferences also disabled the mode and restored its native values. Premium start/expiry timestamps were unchanged. Exercised the Profile toggle at 640×480 as well.

## Solid 3D totems (1.12.0)

- Replaced all five generated-sprite models with explicit closed cuboid meshes, with six faces per part and estimated side/back UV mappings. Structural checks verified positive X/Y/Z extents for every cuboid and no `minecraft:item/generated` parent. Models have 8–19 cuboids (48–114 faces).
- Built and launched the real Member and Premium release JARs in Minecraft 1.21.11 / Fabric Loader 0.19.3 on Java 21.
- A development-only observer queried the actual native ItemStackRenderState bounding box in NONE context. Depths were Drdonut 0.25, Jettism 0.27, Farex 0.30, Hoozar0 0.275 and Jack 0.26875 blocks/model units. These are solid head/body volumes, rather than the old thin generated item extrusion.
- Repeated native model/texture probes across all ten ItemDisplayContexts for all five selections. Original stack components, count, custom name and glint were unchanged, and a diamond continued to use its native model.
- Visually inspected the actual 3D pack previews, both first-person hands, inventory/hotbar, third-person hold and native activation animation. Improved GUI lighting and removed accidental face-colour patches from the estimated side/back hair areas.
- Pack previews now use cached private Paper stacks with an explicit preview model; the Totem-only render override does not alter them or cause every preview to match the equipped style. No preview stack is added to inventory or sent to a server.
- Confirmed native selection and rendering with Performance Mode enabled. Both editions have identical implementation and model data, and the existing Premium start/expiry dates were preserved.

Source authoring is in tools/generate_totem_models.py and modifies model JSON/UV mappings only. Side/back appearance is an estimate from the reference colours and clothing. Test fixtures and synthetic input remain excluded from the distributed files.

- Reloaded resources with F3+T in the final Premium build and rechecked Jack's native model depth, all rendering contexts and previews. Unequip restored the original Minecraft totem model in all contexts. No missing-model/texture or model-parsing errors appeared.


## Jamble hotbar tracking (1.13.0)

- Built Member and Premium release JARs with Java 21 for Minecraft 1.21.11 / Fabric Loader 0.19.3. Ran the packaged, remapped JARs in the real production client, using a separately remapped development-only observer.
- The pure number rules passed all 81 Host/Viewer combinations. Host 5.1 beats Viewer 5; Viewer 8 beats Host 2.1. Null, 0/10, leading zeros, other decimals, non-ASCII digits and names with extra words are rejected. Colour formatting on valid custom names is accepted.
- Exercised the actual Right Shift → Jamble switch, saved preference, instructions, default Off, disable clearing and re-enable baseline. Items already present at enable/login do not create a round.
- Injected inventory updates using the excluded observer to cover consecutive packet arrivals, same-item Host/Viewer stacks, stacked-count increases, expired pairing windows, multiple same-side items, invalid names, slot rearrangement, renaming without acquisition and main-inventory/offhand transfers. The eligible pairs scored once; ambiguous and invalid cases did not score. Result icons use copies with display count 1.
- Used real vanilla server commands to spawn named Diamond and Emerald item entities at the player in the singleplayer test world. Actual pickup into the hotbar produced Host 5.1 / Viewer 5, the correct native item icons and Host Wins! The production mod does not create items or issue these commands.
- Visually inspected both winner messages, the numeric cards and icons, page instructions, 1280×720 and 640×480 layouts. Spotify moves below the cards on compact windows; the watermark moves away or temporarily hides before the hotbar. The centre result is a brief overlay above other HUD content.
- Confirmed F1 and the debug overlay hide the Jamble overlay. Tested with existing Bubble Font, Spotify/lyrics HUD and Performance Mode enabled.

The tracker matches read-only inventory acquisitions by custom name and count. It does not identify which dispenser/block supplied an item. Eligible arrivals must fall within two seconds, after a one-second initial inventory baseline. These are client observations, not server-authoritative match results. Test fixtures, worlds, commands and synthetic-input scripts are excluded from both distributables. Live Windows Spotify is unchanged and remains unverified on the Linux test host.

- Restarted the packaged Premium build with Jamble enabled and a real named pair already in the hotbar. The saved switch remained On, both original item counts/names survived and no false round appeared. A fresh actual pickup then scored normally, and the overlay disappeared after its eight-second display period. Existing Premium start/expiry dates were unchanged. Both edition archives have identical implementation/assets, the exact original nested Freelook hash, no observer classes and the retained five solid totem models.

## Mirrored offhand pose (1.13.1)

- Corrected the five models' authored left-hand yaw from +25 to -25 degrees. Minecraft applies its own left-hand mirror. Meshes, UVs, textures and other display contexts are unchanged.
- Exercised Minecraft's actual ItemTransform.apply and PoseStack for all five models. Left/right front normals are mirrored, both face the player, and the old-release +25-degree regression control fails this check.
- Ran the packaged Member JAR in Minecraft 1.21.11 / Fabric Loader 0.19.3 on Java 21. Equipped all five totems and visually checked both first-person hands. Tested both native Left and Right main-hand preferences with Jack and Jettism. Faces remain towards the player. Native model probes passed all ten rendering contexts and original stack/count/name/glint invariants; Unequip restored the native totem.
- Built both editions; their implementation/assets match, and each retains the exact uploaded Freelook JAR. No competing totem resource pack was used.


## Premium sky picker, world lyrics and organisation (1.14.0)

- Built Member and Premium production JARs with Java 21 for Minecraft 1.21.11 / Fabric Loader 0.19.3. Ran both packaged JARs in a real production client, using a separate observer excluded from releases.
- Reorganised the sidebar into Appearance (Visuals, HUD, Spotify HUD), Tools (Essentials, Customize Totem, Jamble), Settings and a bottom Buy Premium entry. Moved Fake Media to HUD and placed the six sky previews on a dedicated Visuals subpage, with Lyrics In Sky below them. Visually checked 1280×720 and 640×480 layouts and their input hit targets.
- With Member edition, deliberately loaded saved custom-sky, sky-lyrics, totem and Jamble preferences. Runtime gates kept the native sky/totem, did not draw sky lyrics and did not create a Jamble round for incoming named items. Preferences remained intact. Checked the labelled Premium pages, sky-preview routing, Discord logo and native confirmation containing exactly https://discord.gg/gazebo. No browser navigation/message/purchase was performed by the test.
- With active Premium, selected all six actual sky panoramas through the preview cards and checked the saved exclusive enum plus real world screenshots. Minecraft sky restored native rendering immediately. Final panoramas are 1024×512 with linear filtering and share their files with the UI previews. The dome is a cached 576-quad upper hemisphere and one indexed draw; it never changes native world light, fog distance, clock or item state.
- A development-only synthetic media/lyrics fixture supplied four original timestamped test lines. Real world-space text followed the line timing independently of the Spotify HUD and its lyric toggle. Visually inspected the smooth transition, larger final font, F1 hiding, blindness hiding and a real stone roof occluding the text through normal depth testing. The fixture does not ship; live Windows Spotify remains unverified on this Linux host.
- Checked native Nether and End rendering with Premium sky/lyrics preferences enabled, then restored the Overworld and its custom sky. Ran real rain/clear-weather commands without mod rendering errors. Shader-pack/Sodium/Iris compatibility and hardware FPS are not claimed by these vanilla Fabric checks.
- Performed F3+T resource reload with the sky active in both the initial and final packaged Premium builds. The cached GPU mesh recreated correctly, with no sky shader/texture/metadata errors. The final client retained slow sky motion when Performance Mode was disabled, and restored the native sky and custom sky again through the picker.
- Created a real eligible Jamble pair while Premium was active. Expired the local test period through the excluded observer: custom sky/lyrics and totem override stopped, pending/current Jamble state cleared, Member rendering returned, and all saved selections were kept. Expired while the totem pack was already open to confirm controls rebuilt into the locked page. Restoring the valid test period re-enabled normal selection/rendering.
- Restarted the final Premium JAR: the selected sky, sky-lyrics preference, Jettism totem and Jamble preference persisted. Original Premium start/expiry timestamps were unchanged. The offhand correction from 1.13.1 is retained for every creator model.
- Exercised reduced-motion navigation and Reset Astra preferences in the final client. Reset restored the native sky, disabled sky lyrics/Jamble and unequipped the custom totem. Native FOV/gamma and Premium start/expiry dates were unchanged.

Runtime data, test worlds, synthetic song/lyrics, observer classes and input helpers are excluded from the JAR and complete source ZIP. Premium remains the separately requested local 30-day edition, without an account service or secure server-enforced entitlement. Test screenshots establish these render behaviours, not a hardware FPS guarantee or a live Windows Spotify session.


## Native window branding and media hardening (1.14.2)

- Changed Minecraft.createTitle at its actual initial-window and update-title call site to exactly Astra Client. Native window icons use the original gold moon logo, resized once through NativeImage into 16, 32, 48, 64, 128 and 256px icons. Windows sets the per-process app ID before creating the window; Windows library initialization is isolated from other platforms.
- Ran the packaged Member JAR in real Minecraft. Inspected the actual X11 WM_NAME and _NET_WM_ICON properties, checked every native icon size and compared its RGB channels with the reference logo. Initial title, world join and a direct Minecraft.updateTitle stayed Astra Client. This host cannot verify the visual Windows taskbar/pinned shortcuts.
- Following a reported Defender alert on 1.14.0, removed the embedded PowerShell script and the encoded/hidden process launcher entirely. New WindowsMediaSession uses documented Windows.Media.Control WinRT interfaces through existing Minecraft JNA dependencies. No script/EXE/DLL is bundled, no child media process is spawned, and no security settings are changed.
- Native JNA callback/vtable tests passed for actual production calls: interface GUIDs and slots, filtering only Spotify, Unicode metadata, playback/timeline/capabilities, correct previous/next/toggle slots/results, missing timelines, empty sessions, invalid session counts, async cancellation/error/timeout and balanced COM/HSTRING/apartment lifetime. COM calls enforce worker-thread ownership. These tests are part of Gradle check via testWindowsMediaAbi, and are excluded from the installable JAR.
- In the actual client, exercised desktop-link/HUD enable, disable and reconnect paths, the non-Windows guard, native branding, navigation and the preserved HUD/lyrics state contract using excluded synthetic data. There were no native-Windows library attempts or new mod errors on Linux.
- Audited installable archive contents and the exact nested Freelook dependency bytecode for process/network/native loading. Only that dependency's ordinary configuration file I/O appeared. Verified no test/observer classes or runtime files were packaged.
- ClamAV 1.5.4, official signed daily 28184 and bytecode 339 databases: no detections on both previous 1.14.0 JARs and the initial replacement Member JAR. The main database download was CDN rate-limited, so coverage is limited. See SECURITY.md and the separate final scan report for the precise result/limits. No Microsoft Defender scan was possible on this Linux host; the actual report is not declared false or cleared.

Live Windows media playback/Defender verification remain outstanding. Native ABI tests and another engine's scan are not substitutes for those checks. Sky-lyrics placement/polish changes requested after branding were paused to prioritise the security report.


## Fixed celestial lyrics and explicit controls (1.15.0)

- Built both Java 21 / Minecraft 1.21.11 / Loader 0.19.3 edition JARs, including the required native Windows media ABI tests. The reviewed media/window implementation is byte-identical to 1.14.2. Only edition metadata differs between Member and Premium.
- Ran the packaged Premium JAR in real Minecraft using an excluded synthetic synchronized-song fixture. The new glyph meshes draw in the native sky pass after sun/moon/stars and before terrain. Actual screenshots confirm larger luminous current lyrics, dim next-line previews, smooth line transitions, and normal terrain/cloud/roof occlusion. Both Minecraft's sky and Northern Echo's worked.
- Explicit Lyrics In Sky: ON/OFF immediately hides/restores text, persists its preference and releases cached glyph meshes on disable. HUD lyrics and the Spotify HUD were both hidden independently during these tests.
- Turning 90 degrees and walking 20 blocks do not change the saved celestial direction/elevation. Set Sky Position captures the current view once; West/35 degrees correctly replaced the initial South/40 degrees. Lyrics leave the view when looking elsewhere, rather than following the camera.
- Native and Bubble Font both rendered. F3+T safely recreated the glyph cache. The cache is bounded to six lines, validates current font atlases and closes resources on reload/shutdown. F1 and unsupported Nether/End dimensions clear the lyric frame/cache; returning to the Overworld restores it.
- Inspected the six previews and the new controls at 1280×720 and 640×480. The saved placement and On/Off preference were checked after a clean restart.

Live Windows Spotify and Microsoft Defender acceptance remain unverified on this Linux host. Synthetic lyric tests establish rendering behaviour, not availability of lyrics for any particular song. Shader packs and hardware FPS are not covered. See SECURITY.md and the release scan report for antivirus coverage/limits.


## Discord capture compatibility (1.15.1)

- Built Member/Premium on Java 21 for Minecraft 1.21.11 / Fabric Loader 0.19.3. Native Windows media ABI tests passed in both builds; the media implementation remains byte-identical to the reviewed script-free 1.14.2 replacement.
- Added optional Discord Capture Mode in Right Shift → Settings. Ran the packaged Member JAR in real Minecraft and exercised its actual On/Off control. The native window title becomes Astra Client | Minecraft 1.21.11 while enabled, retaining the logo. The Windows process taskbar-ID override was removed as a compatibility precaution, without claiming it was the cause of the reported black stream.
- Native AFK timing was set beyond ten minutes only in an excluded test observer. With capture mode Off, a native FramerateLimitTracker returned LONG_AFK / 10 FPS. On returned NONE / the unchanged 120 FPS user cap. Disabling restored the original throttle. Minimized windows retain native handling; they are not claimed captureable.
- Sent an actual focus-out event to the Minecraft window. While unfocused, Minecraft remained unpaused, the integrated world's time advanced and actual world-render frame count rose from 41 to 70 over the measurement. This verifies continued rendering, not a Windows Discord capture.
- Entered native fullscreen, enabled capture mode, verified the actual native window and fullscreen option became windowed, then disabled it and verified both restored fullscreen. Pause settings restored correctly; a deliberate native pause-option edit was preserved.
- Confirmed that the mode and original settings backup save in Astra's config. Restarted the packaged Premium JAR: capture mode loaded On with the original pause/fullscreen backup intact, and turning it Off restored the original options and title. Reset also disabled the mode and restored the native preferences. Visually checked the Settings page at 1280×720 and 640×480; both compact On/Off hit targets worked.

No Windows Discord receiver or live stream was available on this Linux test host. These checks establish application-side fullscreen/focus/AFK behaviour; successful capture with a particular Discord version, GPU/driver or capture method requires a live Windows retest. No Discord account, messages, native capture injection or security bypass is used.


## Smaller, higher Jamble result banners (1.15.2)

- Reduced Host Wins! and Viewer Wins! text scale from 2.1 to 1.2, the banner height from 38 to 22 GUI units and its horizontal padding from 30 to 20. The banner sits below the top cards, or below the Spotify/lyrics HUD when those are flanked by the cards. It no longer occupies the screen centre. Existing colour, fade and duration remain.
- On narrow screens Spotify moves below the banner only while the result is displayed. Its shared height calculation accounts for scale and the lyrics panel, preventing overlap with the result. Checked the compact layout against the hotbar.
- Built both editions with Java 21 / Minecraft 1.21.11 / Fabric Loader 0.19.3 and the required Windows media ABI checks. Archive comparison confines changes to the JambleHud class family, a SpotifyHud height helper and version metadata. Other feature implementations and original Freelook dependency are retained.
- Ran the packaged Premium JAR in real Minecraft. Both Host 5.1 versus Viewer 5 and Host 2.1 versus Viewer 8 produced the expected result. Inspected all four actual screenshots at 1280×720 and 640×480 with Spotify HUD and lyrics enabled. Tracker tests, world and synthetic observer are excluded from the distributed artifacts.

This is a layout change, not a new scoring rule. Existing Windows Discord/Spotify and Defender verification limits remain as documented in SECURITY.md and the scan report.


## Essentials Fullbright (1.16.0)

- Added a saved, default-Off Fullbright switch below Freelook in Essentials, available in Member and Premium. The client lightmap uses a white clear at the native update cadence. Off/reset invalidates the lightmap and resumes the native lighting path; no gamma or potion manipulation is used.
- Built both editions on Java 21 / Minecraft 1.21.11 / Fabric Loader 0.19.3, including the required Windows media ABI checks. Archive comparison confines changes to Fullbright, its mixin, configuration/menu/version data and the two added client entries in the standard Loom manifest. Edition differences remain metadata-only. Original Freelook is retained; no scripts, native executables or fixtures are bundled.
- Ran the packaged Member JAR in actual Minecraft. A test-only observer created a sealed stone room with block light 0 and sky light 0. Read the actual 16×16 GPU lightmap: native Off had 0 all-white pixels, On had 256, and Off again returned to 0. Actual screenshots show the room dark/bright/dark.
- The real Essentials switch, Reset and compact 640×480 control all worked. Minecraft gamma remained exactly 0.37 throughout; menu brightness, Freelook binding and world light levels were unchanged, and no Night Vision effect was added. Inspected the normal/compact Essentials layout and description.
- Stopped Member cleanly with Fullbright On, then started the packaged Premium JAR. The saved setting loaded On and all 256 lightmap pixels were white. Premium UI Off/On restored native/full lightmap respectively, with gamma unchanged. F3+T resource reload retained Fullbright and its correct lightmap without mod errors.

The synthetic observer, room-creation commands, native texture readback and screenshots do not ship. No hardware FPS or shader-pack compatibility claim is made. Existing live Windows Discord/Spotify and Microsoft Defender verification limits remain in SECURITY.md and the scan report.


## Receipt-only compact Jamble and native win buttons (1.18.0)

- Reworked the cancelled prototype following the owner's new request. Version 1.17.0 remains withdrawn. Both 1.18.0 editions built for Java 21 / Minecraft 1.21.11 / Loader 0.19.3, including Windows media ABI tests and money/ledger/layout contracts.
- Pure contracts passed exact K/M/B amounts, limits, FIFO association, exact 2x, duplicate/stale/overflow/session handling and 864 compact-layout combinations. Added checks that idle play retains native Spotify scale and receipt/toast rectangles remain separated above the native HUD.
- Ran the packaged Premium JAR in Minecraft. With Jamble On and no payment, no Jamble card/toast appeared, J did not open a window, and an unpaid Viewer-winning hotbar roll still produced no HUD. A new qualifying receipt showed just one compact card.
- J opened the cursor-enabled review screen. Before a roll, Await roll was disabled and a real mouse click made no payout. J closed the screen without reopening it. Host-winning receipts expired from the HUD. A native chat Review click also opened the correct payer's screen before their roll.
- Actual native hotbar roll Host 2.1 / Viewer 8 enabled BetaUser's Mark won button for a 2.5M receipt. A real mouse click recorded exactly 5M and changed it to disabled Recorded; another click did not duplicate the payout. Previous/Next correctly changed the selected payer while keeping the captured payment UUID stable.
- Closing review showed a short payout toast; after expiry both card and toast were gone. Inspected full-size screenshots of the minimal receipt, inline result, real review button and empty completed state.
- Repeated at 640×480 with saved Spotify size 100%. A 3K receipt won Viewer 9 / Host 1.1, its real native button recorded 6K, receipt/toast bounds stayed separated, then both disappeared. Spotify returned to its native width-fit scale while the saved 100% preference remained unchanged.
- Restarted the packaged Premium JAR: no historical HUD/window appeared, exact payment limits persisted and J with no receipt stayed inactive. A new receipt activated the card; Right Shift → Jamble → Payments opened the same native review screen and Escape returned correctly to its parent menu.

The first instrumentation run failed in the excluded observer because a Minecraft inherited-method call was not remapped through the custom subclass. Casting to the Minecraft Screen type fixed that test helper; production code did not require a change. Final native interaction tests passed. The observer, synthetic usernames/receipts and test worlds do not ship. Live authenticated DonutSMP and Windows Discord/Spotify/Defender remain unverified; the security/scan reports retain those limits. All confirmations are local records, with no automatic currency transfer.


## PvP page and own-player HUD (1.19.0)

- Built Member and Premium with Java 21 / Minecraft 1.21.11 / Fabric Loader 0.19.3. Required Windows media ABI and Jamble contracts passed, including the existing 864 receipt-layout combinations.
- Launched the remapped production Premium JAR in Minecraft. Native mouse clicks opened the bottom-right PvP arrow, all eight mode categories, all twenty custom switches, the native Damage Tilt slider and HUD scale slider. Both slider ends changed the actual values. Duplicate settings shared state across modes. Client/PvP navigation remembered each page's category with animations both On and Off. Original Essentials/Fullbright and Visuals content remained accessible. Right Shift and Escape worked without crashing.
- Native fixture checks verified custom settings default Off, config validation/clamping, JSON roundtrip and 135 HUD-bound combinations across five viewport sizes, three scales and nine anchor positions. Actual inventory/offhand crystal counts were 67 (64+3, no duplicate); potion/arrow variants, enchanted/regular apples, exact sword durability and equipped armor values matched native client state.
- Runtime particle tests returned no particle for EXPLOSION and EXPLOSION_EMITTER while the filter was On, still created unrelated FLAME particles and restored explosions when switched Off. Actual burning renders showed flames lowered with Low Fire On and native-height flames when Off. No damage/sound/world/block logic was changed.
- Used real native mouse dragging to move the PvP panel, verified clamped saved coordinates and edited scale from 60% to 100%. Fixed the HUD editor's instruction placement to avoid the Spotify header and made its buttons receive clicks even when the dragged HUD overlaps them. The editor resets position and returns to the same parent menu.
- Restarted with the final packaged Member edition. All saved PvP switches, size and position persisted, with Premium inactive. Native context checks passed unloaded/loaded crossbow state, shield durability, fall distance, food/saturation, active-use timer, Minecraft bow-power calculation and an own Speed II effect with a 1:00 timer.
- Repeated real page-arrow, category/toggle and editor clicks at 640x480. Verified compact bounds, Reset position, Done click priority through an overlapping large HUD, original page content, empty editor preview without enabling modules, F1 hiding the HUD and a two-counter gameplay panel. The small-window screenshot caught an overlap with Spotify at the original default anchor; the final default/reset anchor was moved lower and rechecked. Inspected screenshots at 1280x720 and 640x480. Only enabling many options deliberately produces many rows; custom controls ship Off.
- Archive checks passed: no runtime scripts/executables/test fixtures, original nested Freelook hash unchanged, existing native Windows media bytecode unchanged, Member/Premium code identical apart from edition/version metadata. Changes to existing classes are limited to client initialization, settings, menu/navigation and menu icons; all remaining new classes belong to PvP settings/HUD or the two visual mixins.

Tests ran in Minecraft on Linux/software rendering with an excluded observer and local creative test world. They are not Windows/GPU FPS benchmarks or a live DonutSMP server test. Test fixtures, synthetic inventories/effects, worlds and runtime settings do not ship in the JAR or source ZIP. Microsoft Defender verification remains pending as documented in SECURITY.md.
