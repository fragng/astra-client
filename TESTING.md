# Astra Client 1.19.1 validation

This release removes the Jamble payment features and restores the original hotbar-only Jamble, while preserving the PvP page and the rest of Astra.

## Build and archive checks

- Built both Member and 30-day Premium for Java 21, Minecraft 1.21.11 and Fabric Loader 0.19.3. Started with a clean build so deleted payment classes cannot remain in the output. Both builds passed the required native Windows media ABI tests (Spotify selection, metadata, timeline/controls, command slots, async cleanup, bounded sessions and COM ownership).
- The JambleHud and SpotifyHud source files exactly match the published pre-payment 1.16.0 source. Only five production class families differ from 1.19.0: AstraClient, AstraConfig, ClientMenuScreen, JambleHud and SpotifyHud. PvP and all other existing code match 1.19.0 byte-for-byte.
- JamblePayments, JamblePaymentLedger, JambleMoney, JambleReviewScreen and their nested classes are absent from both installable JARs. Their initialization, chat listener, client commands, J binding, config limits and UI integrations have been removed. The obsolete payment-specific test/task and instructions were removed as well.
- Archive integrity passed, with no runtime scripts, native executables or test fixtures. Both editions have identical code and assets, differing only in version/edition metadata. The original nested Freelook 1.2.8 hash is unchanged: fe1a32d9e4b8894122f52985c9d81b5cefa7bb7b67e67d17e8d03c495f8ba1e4.

## Actual Minecraft checks

Ran the packaged Premium JAR in Minecraft with an excluded observer and a local creative test world:

- Checked all 81 Host/Viewer comparisons, including the Host's .1 advantage on matching base numbers, plus invalid name rejection outside the exact 1–9 and 1.1–9.1 formats.
- With Jamble enabled and no payment or completed roll, there was no Jamble HUD. The native keybinding registry contained no Jamble keybinding, and pressing J opened no screen.
- Opened Right Shift → Jamble using real native mouse input. The original toggle and hotbar instructions were present; Payment Limits and Payments/review buttons were absent. Real On/Off clicks changed the setting and cleared the current result.
- Received Host 5.1 and Viewer 5 in the hotbar without any payment: the original cards displayed the diamond/emerald icons, Host won, and the display expired automatically. A separate Host 2.1 / Viewer 8 pair showed Viewer Wins. J still did not open a screen during either result.
- Main-inventory receipts and moving those same items into the hotbar did not create a new roll. The original acquisition safeguards remain.
- Verified that the retained bottom-right PvP navigation still opens Crystal PvP with Low Fire and its other controls.
- Repeated an unpaid Host 3.1 / Viewer 9 roll at 640×480 with default Spotify size. The original small winner result appeared near the top and Spotify moved below it as before. Inspected full-size and small-window screenshots.
- Saving retained jambleEnabled and removed the obsolete Jamble payment-limit fields from the config. Other Astra settings stayed present.

Fixtures, synthetic test items, runtime configuration, screenshots and worlds do not ship. Startup and animation timing needed adjustment in the external test runner; production code did not require changes for those test-helper waits. This was a Linux/software-rendering check, not a live authenticated DonutSMP or Windows integration test. Defender verification remains pending; see SECURITY.md and the separate limited-coverage scan report.
