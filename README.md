# Astra Client 1.6.1

Cosmetic Fabric client for Minecraft Java **1.21.11**, **Java 21**, **Fabric Loader 0.19.3+**, and **Fabric API 0.141.6+1.21.11**.

[Download Astra Client 1.6.1.jar](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.6.1.jar)

Replace your previous Astra jar in the mods folder. Press **Right Shift** in a world to open the menu.

## Inventory hover rendering fix

Removed the standalone Music category and its volume/mute controls. Spotify HUD remains a separate category, and Minecraft's native sound settings are kept.

Rounded inventory slots, hover highlights and tooltip backgrounds now use cached GUI-atlas sprites instead of rebuilding many small rectangles per frame. In an instrumented 54-item chest test, hovering/sweeping submitted **881 GUI elements per frame, down from 8,810**. This is a GUI-element measurement from a software-rendered development host, not a hardware FPS guarantee. Tooltips, item content and rounded styling were checked after a resource reload.

## Spotify HUD category

All Spotify controls now live in **Right Shift → Spotify HUD**:

- Enable Spotify HUD and Enable Lyrics.
- Desktop link and Reconnect.
- HUD size (50–100%, default 70%).
- Song/connection status, Previous, Play-pause and Next.
- **Customise Spotify HUD:** Galaxy, Astra, Nebula or Black, with a live preview and saved independent theme preference.

The top-centre card now uses a compact text-only layout: no album artwork or music icon. Lyrics glide vertically between lines with fading and a gradual highlight. Seeks and track changes select the correct lyric immediately. Smooth animations can be disabled in Settings.

HUD holds Astra watermark preferences, and Settings holds general client preferences. The standalone Music category and its controls are removed. The Bubble Font switch remains in Visuals.

Open the Windows Spotify desktop app and play a song. Close the client menu to see the HUD. Lyrics use LRCLIB and require internet and catalogue availability; no Spotify login is requested. Metadata lookup sends song title, artist, album and duration to LRCLIB. Missing lyrics or timing have clear status messages.

## Validation

Built and exercised inside Minecraft on Linux: seven-page navigation, moved preferences, size, four distinct theme previews and in-game backgrounds, compact layout and lyric transition frames. Lyric motion tests check frame-rate independence, seeking and reduced motion. The Windows helper loop was tested with mocked sessions; live Windows Spotify playback remains unverified on this Linux host. Development fixtures are excluded from the download.

[Download source, full documentation and build instructions](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.6.1-source.zip)
