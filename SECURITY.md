# Astra Client 1.33.0 security status

**26 November 2026: the reported Windows detection is unresolved.** The user described the latest 1.32.0 alert as “Trojan.Severe”; the complete Defender identifier and affected filename/hash were not supplied. The 1.32.0 installable JARs remain withdrawn. Version 1.33.0 is a requested feature preview, not a verified remedy. Neither malware nor a false positive has been established. Do not disable protection, add exclusions or restore a blocked file to run this preview.

## Changes requiring review

- The exact user-supplied CreamyKeys Universal 0.0.5 JAR is now nested, SHA-256 `023767afb373dcf16f0e0768d358e253fc072ebd3719d7609772c8057d094730`. It bundles the matching original CreamyKeys 0.0.5 implementation and JLayer. Astra's former sound engine and keyboard/mouse mixins were removed. The original mod uses OpenAL/JNA; its native settings page and enable/disable audio behavior were tested in Minecraft.
- MCEF Modern 0.3.3, SHA-256 `5d7b0da06c97085fde4f76bc1b98fe2765a270a006dd8b37d903bd479eb27dda`, supplies JCEF/Chromium for the real Krillion website. First use downloads/caches platform-specific native browser components and starts CEF helper processes. Those native components are **not** covered by a scan of the distributable JAR alone. Ordinary client use does not start the browser. The JCEF runtime's platform sandbox behavior has not been independently certified; do not treat this as a hardened general-purpose browser or use it for sensitive accounts.
- Astra removes the upstream `--disable-web-security`, Widevine and autoplay exceptions. TLS validation stays enabled. Main-frame navigation is restricted to HTTPS krillion.io origins; other HTTPS links use Minecraft's confirmation. Downloads are cancelled and no Minecraft JavaScript/native bridge is exposed. The website still executes its own scripts and network requests like any live website.
- Wordle's new screen uses the existing local game/save rules. The reveal clock is presentation only. Case rewards, licensing and private owner keys are unchanged.

The earlier claim that Freelook is the only nested dependency, and that the entire client never downloads or starts a helper, applies to older releases only. The Windows Spotify bridge itself still uses direct WinRT/JNA without its former PowerShell launcher.

## Verification and limits

Java 21 builds and required contracts pass. Native Linux Minecraft checks cover the exact CreamyKeys settings/audio and Wordle's larger board, sequential reveals, reduced motion, input gating and saved progress. Browser initialization/download and rendering were observed; the cloud proxy certificate prevented validating live Krillion gameplay. No certificate-check bypass was used. Windows Spotify/browser behavior and Defender clearance are not live-tested on this Linux host.

The full official ClamAV main63/daily28194/bytecode339 scan of 1.32.0 found no detections. That does not clear Defender or prove the new browser runtime safe. See the versioned scan report for the exact final 1.33.0 artifact scope and [the earlier investigation](downloads/INVESTIGATION-1.32.0.txt). Report a fresh alert with the complete Protection history threat name, affected filename and SHA-256; keep the block in place.

The complete source includes upstream dependency source and licenses where supplied; see [THIRD_PARTY.md](THIRD_PARTY.md). No private issuance key is included.

## Archived security history through 1.32.0

The following historical statements describe their named versions and do not replace the current browser/download disclosure above.

## Replacement implementation

The prior Windows Spotify integration launched a bundled PowerShell script using an encoded command and hidden window. It read Windows media sessions, but that unnecessary execution mechanism can resemble patterns security products flag. Version 1.14.2 removed the script and process launcher entirely and uses the Windows Media Control WinRT APIs directly through Minecraft's existing JNA dependencies.

The installable JAR contains no PowerShell/batch/shell scripts or EXE/DLL files. The media bridge does not disable protection, create exclusions, bypass execution policy, add persistence, install a service, start a child process or download/run a helper. The Java source remains readable and included. The only bundled mod dependency is the exact original Freelook 1.2.8 JAR, SHA-256 `fe1a32d9e4b8894122f52985c9d81b5cefa7bb7b67e67d17e8d03c495f8ba1e4`; its bytecode was reviewed for process/network/native loading, with only its normal configuration file I/O found.

Astra's lyric service uses HTTPS to LRCLIB with the selected song's title/artist/album/duration. The Discord link opens through Minecraft's native user confirmation. Other custom preferences stay in the instance's config directory. Astra 1.15.1 removes the per-process Windows taskbar app-ID override; the bundled window logo remains. No registry or pinned-shortcut changes are made.

Version 1.19.1 removes the Jamble payment listener, client commands/chat links, J-key review screen and keybinding, payment ledger, stake-limit preferences and payout HUD/records. The original read-only named-item hotbar tracker and Host/Viewer result renderer are restored byte-for-byte from the last pre-payment source (1.16.0), together with its Spotify layout integration. No payment receipt is required for a roll. The PvP page from 1.19.0 remains, along with the existing native media bridge, exact Freelook dependency, capture mode, Fullbright, skies and totems. No new network endpoint, executable, child process or native dependency is introduced. Version 1.17.0 remains withdrawn. Defender verification remains pending.

Version 1.20.0 adds two bundled PNG wallpapers, a shared local six-theme transition renderer and adaptive selectors. It uses cached Minecraft textures and fixed-size animation state; it adds no download endpoint, process, native library, credential or gameplay action. The original Jamble rollback remains in place. Media, PvP, skies, totems, capture and Freelook code are unchanged from 1.19.1.

Version 1.21.0 adds six locally authored 3D character models, a saved exclusive cosmetic choice and three renderer/access mixins. They replace only the local player model, its matching texture and first-person hands, restoring the original renderer afterward. Other players, account skins, hitboxes, eye height and equipment data are unchanged. Character gear layers are cosmetically suppressed while held items remain visible. Assets are bundled JSON/PNG and cached native geometry; no new endpoint, account access, model download, process, executable or native dependency is introduced. Backgrounds, original Jamble, PvP, media and the exact Freelook dependency are retained.

Version 1.22.0 refines those same six local cosmetics with curved surfaces and analytic lighting normals. A native ModelPart.Cube subclass emits cached vertices through Minecraft's existing vertex API; native articulated bones, texture scope and renderer restoration remain in place. Native skin-preview rendering displays the same curved geometry with separate pose instances. Assets remain bundled JSON/PNG. No new network endpoint, process, account permission, native library or gameplay action is introduced. Existing Jamble, media, PvP, skies, capture, totems and Freelook code remain unchanged.

Version 1.23.0 adds shallow cosmetic pores/material shades, a saved first-person Small Totem switch and optional event-driven character speech. Speech is 324 bundled Ogg clips, generated during development from the CC BY 4.0 Piper/VCTK model with new original dialogue; model/source/attribution are documented in CHARACTER_VOICES.md and inside the JAR. Python, Piper, ONNX models and FFmpeg are development-only and do not ship or run with the mod. Native sound playback uses the Voice/Speech category; there is no microphone access, speech-service request or helper process. Local ticks and native packet/action observation request only cosmetic audio, without generating attacks, inventory actions, chat, commands or server packets. Weather/combat/group controls, volume, cadence and Small Totem are saved locally. Original Jamble, media, PvP, skies, capture, totems and exact Freelook remain intact. No new runtime endpoint, executable or native dependency is introduced.

Version 1.24.0 doubles speech to 648 clips, adds character-inspired pitch/timbre processing and a public-domain LJ Speech voice for Sandy, and enables speech automatically on character selection. DrDonutt retains an original generic voice, with no imitation of his actual voice. All synthesis/effects are baked into the Ogg resources during development. Runtime mouth animation interpolates bundled RMS amplitude samples; no audio capture, runtime synthesis or signal analysis occurs. Cached articulated eyelids, sweat beads and gentle breathing are local cosmetics using the existing renderer scope. Sweat observes only the local player's sprint/fire/health state. One-time legacy voice migration and subsequent explicit Off preferences save locally. The header uses the existing bundled moon logo. No new runtime endpoint, microphone access, process, native dependency or gameplay action is introduced.

Version 1.25.0 adds a native-font alias and cached render-only copies for glowing sign text, plus stronger shared background camera/blend transitions on the title/client menus and Spotify HUD. The sign renderer preserves original world/server data and explicit custom fonts; resource reload clears the weak cache. Rendering uses existing local textures and fixed-size animation state. No new runtime endpoint, executable, native dependency, gameplay action or server packet is introduced. Character speech/models, original Jamble, PvP, custom skies, totems, native media and exact Freelook remain unchanged.

Version 1.25.1 replaces the displayed Discord invite and the confirmed Discord link destination with .gg/astrayt. Rendering and gameplay behaviour are otherwise unchanged.

## What was verified

- Java 21 / Minecraft 1.21.11 / Fabric Loader 0.19.3 builds and real Linux Minecraft UI/native-window checks.
- Real native JNA callback/vtable tests for GUIDs/slots, Spotify filtering, UTF-16 metadata, timeline/controls, command results, async failure/cancellation/timeout, bounded session counts and COM/HSTRING/apartment cleanup. Run `./gradlew testWindowsMediaAbi` or `./gradlew check`.
- Archive inspection for unexpected scripts/native executables and nested dependencies. Test fixtures and runtime data are excluded from the installable JAR.
- ClamAV 1.5.4 using verified official daily database 28184 (15 Nov 2026) and bytecode database 339. The main database download was CDN rate-limited; no bypass/retry of that cooldown was attempted. This is limited signature coverage, not a full antivirus assurance. The scan of the previous 1.14.0 JARs also found no detections, which does not invalidate the reported Defender alert.

## Limits and reporting

Live Windows Spotify and Microsoft Defender were not available on this Linux test host. Native ABI-contract tests are not a live Windows integration test. Microsoft Defender may apply different signatures or cloud reputation. There is no guarantee that any antivirus will accept the file.

Keep Defender and browser protection enabled. Do not restore a quarantined download, add an exclusion, rename/disguise the file to evade scanning, or turn protection off to use Astra. If a replacement is flagged, keep the block and record the exact Protection history threat name, affected filename, version and SHA-256. Compare against the published SHA256SUMS file and use only the public repository's download links. A vendor false-positive submission requires that concrete information and can be made through Microsoft's official file-submission service.

The complete source ZIP naturally includes standard Gradle build scripts; the no-scripts statement above describes the installable mod JAR, not the developer build tools.
