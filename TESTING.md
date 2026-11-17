# Astra Client 1.20.0 validation

## Build and deterministic contracts

- Built Member and 30-day Premium for Java 21, Minecraft 1.21.11 and Fabric Loader 0.19.3. Required native Windows media ABI checks passed.
- New `testSceneTransitions` also runs in `check`: 108 ordered theme-pair/frame-rate endpoints, normalized full-coverage blends, decreasing outgoing offsets (leftward travel), completion and reduced-motion snapping. Checked 10,000 interrupted retargets for finite normalized weights and continuity of visible positions/colors at each retarget.
- Verified 80 title-panel viewport combinations. All six rows and Reactive Background fit inside their panel with margins, including short layouts. Longer mode labels scale within the available space rather than touching their switches.

## Packaged Minecraft runs

Ran the remapped Premium and Member JARs on Linux/software rendering, with an excluded observer:

- Real native title-screen clicks selected all six themes: Normal, Galaxy, Nebula, Astra, Sunset and Beachy Sands. New bundled wallpapers loaded at full 1672x941 size, rather than missing-texture placeholders. Normal returned to Minecraft's live panorama.
- Inspected title screenshots for all themes and a mixed Galaxy/Sunset frame. During travel the selected destination had a positive incoming offset, both scenes had nonzero blend weights, and settling left the chosen scene at full weight. Repeated rapid selections retained normalized coverage and finished at the latest choice.
- Repeated native title selection and bounds checks at 640x480. All six modes and Reactive Background remained visible inside the right-hand panel, with a screen-edge margin.
- Opened the actual local world and Right Shift menu. Its 3x2 selector showed all six choices inside the rounded panel. Real clicks switched every theme, with a sampled mixed Sunset frame and correctly settled endpoints. Checked the smaller in-game layout at 640x480. Reactive Background/Bubble Font remained usable below the theme grid.
- Smooth animations Off and Performance Mode On produced an immediate settled selection on the next rendered frame. Re-enabling ordinary animations restored travel. Turning Performance Mode Off restored its backed-up native settings.
- Saved Beachy Sands, restarted with the Member edition and verified it loaded at full weight. Reloaded Minecraft resources, then switched between both new themes with valid textures. Entered the world again, used Right Shift and both new choices, then clicked Minecraft's actual Save and Quit to Title button. It saved the world and returned to the same Beachy Sands title screen.

The observer needed to wait for rendered state rather than merely the earlier config/input tick, and to identify native screens by their actual buttons because production Minecraft class names are remapped. An early external helper directly invoked a force-rendering disconnect from inside a tick; that instrumentation run was stopped after it stalled the software renderer. The subsequent test used the real native pause-menu button and passed. No production code change was required for those helper issues. Fixtures, test worlds, screenshots, runtime configuration and helper commands do not ship.

## Scope and archive checks

- Only background/menu/preload classes and the new SceneTransition class changed. Original JambleHud/JambleRules/SpotifyHud, config serialization, PvP, media and other existing production classes match 1.19.1 byte-for-byte. Jamble payment/review/money classes remain absent.
- Archive integrity passed. Member/Premium share identical code/assets and differ only in version/edition metadata. Both new wallpaper files match the generated originals. No runtime scripts, native executables or fixtures were added. The exact original nested Freelook 1.2.8 hash remains fe1a32d9e4b8894122f52985c9d81b5cefa7bb7b67e67d17e8d03c495f8ba1e4.
- No per-frame image decode, GPU texture upload or offscreen render-target allocation is introduced by the background renderer. Fixed-size transition arrays cover at most six cached scene textures; settled rendering uses the selected scene. Texture lookup uses Minecraft's resource manager after reloads.

These are functional/rendering checks, not GPU FPS benchmarks or live authenticated DonutSMP/Windows tests. Windows Spotify and Microsoft Defender were unavailable. Existing security review limits and the separate limited-coverage scan report still apply.
