# Astra Client security review — 1.19.1 (script-free bridge retained from 1.14.2)

A Microsoft Defender threat alert was reported by a friend of the client owner for the latest public version (1.14.0). The exact Defender detection name, affected filename and file hash were not available. The report is taken seriously; the recommended download links were paused during investigation, and both 1.14.0 installable JARs were withdrawn from the default branch (source/history retained). No claim is made that the report was a false positive or that Defender has cleared the replacement.

## Replacement implementation

The prior Windows Spotify integration launched a bundled PowerShell script using an encoded command and hidden window. It read Windows media sessions, but that unnecessary execution mechanism can resemble patterns security products flag. Version 1.14.2 removed the script and process launcher entirely and uses the Windows Media Control WinRT APIs directly through Minecraft's existing JNA dependencies.

The installable JAR contains no PowerShell/batch/shell scripts or EXE/DLL files. The media bridge does not disable protection, create exclusions, bypass execution policy, add persistence, install a service, start a child process or download/run a helper. The Java source remains readable and included. The only bundled mod dependency is the exact original Freelook 1.2.8 JAR, SHA-256 `fe1a32d9e4b8894122f52985c9d81b5cefa7bb7b67e67d17e8d03c495f8ba1e4`; its bytecode was reviewed for process/network/native loading, with only its normal configuration file I/O found.

Astra's lyric service uses HTTPS to LRCLIB with the selected song's title/artist/album/duration. The Discord link opens through Minecraft's native user confirmation. Other custom preferences stay in the instance's config directory. Astra 1.15.1 removes the per-process Windows taskbar app-ID override; the bundled window logo remains. No registry or pinned-shortcut changes are made.

Version 1.19.1 removes the Jamble payment listener, client commands/chat links, J-key review screen and keybinding, payment ledger, stake-limit preferences and payout HUD/records. The original read-only named-item hotbar tracker and Host/Viewer result renderer are restored byte-for-byte from the last pre-payment source (1.16.0), together with its Spotify layout integration. No payment receipt is required for a roll. The PvP page from 1.19.0 remains, along with the existing native media bridge, exact Freelook dependency, capture mode, Fullbright, skies and totems. No new network endpoint, executable, child process or native dependency is introduced. Version 1.17.0 remains withdrawn. Defender verification remains pending.

## What was verified

- Java 21 / Minecraft 1.21.11 / Fabric Loader 0.19.3 builds and real Linux Minecraft UI/native-window checks.
- Real native JNA callback/vtable tests for GUIDs/slots, Spotify filtering, UTF-16 metadata, timeline/controls, command results, async failure/cancellation/timeout, bounded session counts and COM/HSTRING/apartment cleanup. Run `./gradlew testWindowsMediaAbi` or `./gradlew check`.
- Archive inspection for unexpected scripts/native executables and nested dependencies. Test fixtures and runtime data are excluded from the installable JAR.
- ClamAV 1.5.4 using verified official daily database 28184 (15 Nov 2026) and bytecode database 339. The main database download was CDN rate-limited; no bypass/retry of that cooldown was attempted. This is limited signature coverage, not a full antivirus assurance. The scan of the previous 1.14.0 JARs also found no detections, which does not invalidate the reported Defender alert.

## Limits and reporting

Live Windows Spotify and Microsoft Defender were not available on this Linux test host. Native ABI-contract tests are not a live Windows integration test. Microsoft Defender may apply different signatures or cloud reputation. There is no guarantee that any antivirus will accept the file.

Keep Defender and browser protection enabled. Do not restore a quarantined download, add an exclusion, rename/disguise the file to evade scanning, or turn protection off to use Astra. If a replacement is flagged, keep the block and record the exact Protection history threat name, affected filename, version and SHA-256. Compare against the published SHA256SUMS file and use only the public repository's download links. A vendor false-positive submission requires that concrete information and can be made through Microsoft's official file-submission service.

The complete source ZIP naturally includes standard Gradle build scripts; the no-scripts statement above describes the installable mod JAR, not the developer build tools.
