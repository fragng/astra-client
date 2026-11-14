# Astra Client

A cosmetic Fabric client for Minecraft Java 1.21.11, Java 21 and Fabric Loader 0.19.3 or newer. Requires Fabric API 0.141.6+1.21.11.

[Download Astra Client 1.5.1.jar](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.5.2.jar)

Replace your previous Astra jar in the mods folder. Press **Right Shift** in a world to open the menu.

## Compact HUD and playback recovery (1.5.2)

The Spotify HUD defaults to 70% of its previous size. **Right Shift → HUD → Spotify HUD size** adjusts it from 50% to 100%; the choice saves automatically.

Fixed progress and synced lyrics freezing when Windows' playback timestamp is older than five seconds. The desktop link now retries after a failed startup or process exit, and artwork errors no longer block song metadata. Startup errors are logged under Astra Spotify in latest.log.

The smaller layout and slider were exercised in Minecraft. Timeline and cover-error handling were tested with mocked Windows sessions; connection lifecycle recovery was tested with real substitute child processes. Live Windows Spotify remains unverified.

## Spotify HUD visibility fix (1.5.1)

The card now appears whenever enabled, including when Spotify is disconnected or has no song title. It shows the connection status and a Reconnect hint. Enabling it from Settings or HUD also enables Desktop link and reconnects if needed. Close the Right Shift menu to view the HUD.

## Spotify HUD

A top-centre card with album artwork, song title, artist, progress bar and playback time, styled after the supplied reference. Lyrics appear below the card.

In **Right Shift → Settings**:

- **Enable Spotify HUD** shows or hides the card.
- **Enable Lyrics**, directly below it, shows or hides lyrics.

Both preferences save automatically. Use the Spotify desktop app on Windows 10/11 and keep **Music → Desktop link** enabled. Playback buttons remain in the Music tab. **Visuals → Bubble Font** still switches between bubble lettering and Minecraft's normal font.

Lyrics use LRCLIB and require internet access. Timestamped lyrics follow playback; plain lyrics are labelled unsynced and cycle for reading. Missing artwork, timing or lyrics use clear fallbacks. No Spotify login is requested. Lyrics lookups send song metadata to LRCLIB.

Built and exercised in Minecraft on Linux with a development-only media fixture. Live Windows Spotify playback/artwork remains unverified; the Windows bridge protocol was tested with mocked sessions. The downloadable mod excludes all testing fixtures.

[Download source, full documentation and build instructions](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.5.2-source.zip)
