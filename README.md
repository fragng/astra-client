# Crystal Client — Single JAR

Crystal Client 1.0.1 packages the complete client into **one installable JAR** for Minecraft Java **1.21.11 / Fabric Loader 0.19.3+ / Java 21**.

## Download

**[Download crystal-client-1.0.1.jar](https://raw.githubusercontent.com/fragng/astra-client/crystal-downloads/downloads/crystal-client-1.0.1.jar)**

Put that JAR directly in your Fabric instance’s `mods` folder. When updating from the earlier six-file Crystal pack, remove its older Crystal JAR and its bundled Fabric API, Sodium, Lithium, FerriteCore and ImmediatelyFast copies first. The new JAR supplies the complete set. Use a separate Crystal game instance.

The complete JAR contains the white Crystal interface, logo, 28 Jack welcome lines, working Fast/Maximum FPS presets, optional actual-FPS HUD, and original unchanged Fabric API/Sodium/Lithium/FerriteCore/ImmediatelyFast components through Fabric’s nested-JAR mechanism. Press **Right Shift** in a world for performance settings.

Tested in actual Minecraft with only the complete Crystal JAR installed, plus an external test observer: all bundled mods resolve, the home/settings UI works, a saved world loads and Right Shift opens/closes settings. The observer is excluded from the release. ClamAV scanned the complete final JAR with zero detections; this does not certify Windows Defender results. FPS gains vary by PC/world.

Licenses, credits and corresponding LGPL source archives are embedded in the JAR. Full client source and build instructions are also available:

- [Source ZIP](https://raw.githubusercontent.com/fragng/astra-client/crystal-downloads/downloads/crystal-client-1.0.1-source.zip)
- [SHA-256 checksums](https://raw.githubusercontent.com/fragng/astra-client/crystal-downloads/downloads/SHA256SUMS-crystal-client-1.0.1.txt)
- [Scan report](https://raw.githubusercontent.com/fragng/astra-client/crystal-downloads/downloads/SCAN-REPORT-crystal-client-1.0.1.txt)
