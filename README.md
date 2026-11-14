# Astra Client

A cosmetic Fabric client for Minecraft Java 1.21.11, Java 21 and Fabric Loader 0.19.3 or newer. Requires Fabric API 0.141.6+1.21.11.

[Download Astra Client 1.5.0.jar](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.5.0.jar)

Replace your previous Astra jar in the mods folder. Press **Right Shift** in a world to open the menu.

## New Spotify HUD

A top-centre card with album artwork, song title, artist, progress bar and playback time, styled after the supplied reference. Lyrics appear below the card.

In **Right Shift → Settings**:

- **Enable Spotify HUD** shows or hides the card.
- **Enable Lyrics**, directly below it, shows or hides lyrics.

Both preferences save automatically. Use the Spotify desktop app on Windows 10/11 and keep **Music → Desktop link** enabled. Playback buttons remain in the Music tab. **Visuals → Bubble Font** still switches between bubble lettering and Minecraft's normal font.

Lyrics use LRCLIB and require internet access. Timestamped lyrics follow playback; plain lyrics are labelled unsynced and cycle for reading. Missing artwork, timing or lyrics use clear fallbacks. No Spotify login is requested. Lyrics lookups send song metadata to LRCLIB.

Built and exercised in Minecraft on Linux with a development-only media fixture. Live Windows Spotify playback/artwork remains unverified; the Windows bridge protocol was tested with mocked sessions. The downloadable mod excludes all testing fixtures.

[Download source, full documentation and build instructions](https://raw.githubusercontent.com/fragng/astra-client/main/downloads/astra-client-1.5.0-source.zip)
