# Astra Client 1.21.0 validation

## Build and archive checks

- Built Member and 30-day Premium for Java 21 / Minecraft 1.21.11 / Fabric Loader 0.19.3. Existing Windows media ABI and six-theme transition/layout contracts passed.
- Archive integrity passed, with identical code/assets between editions apart from edition/version metadata. Only character classes/mixins, custom config and menu/sidebar/icon classes changed from 1.20.0. Original Jamble, PvP, background travel, media and other existing code are byte-identical. Removed Jamble payment/review classes stay absent.
- Six solid item previews plus a SpongeBob head icon use generated native model JSON within the allowed element-coordinate bounds. The six entity models share a 512x512 color atlas and use 213 authored cuboids with positive depth. Source generator and matching geometry are included. No downloaded models, runtime scripts, native executables or test fixtures ship.
- Original nested Freelook SHA-256 remains fe1a32d9e4b8894122f52985c9d81b5cefa7bb7b67e67d17e8d03c495f8ba1e4.

## Actual packaged Minecraft checks

Ran packaged Premium, then the final Member edition, using excluded observation helpers and a local creative world:

- First-page navigation showed nine categories and a clickable 3D Characters page. Six real native switches selected SpongeBob, DrDonutt, Patrick, Squidward, Mr. Krabs and Sandy. Each replaced the previously selected style. Turning the active switch Off restored the normal player/texture.
- Native model checks baked all six models, verified non-flat 3D extents, observed actual leg-pose changes with walk animation and confirmed cached model reuse. Third-person-front screenshots showed each actual in-game character. First-person screenshots showed matching SpongeBob hands and Mr. Krabs claws. Inventory preview rendered the selected model.
- Local render states used the character atlas; a separate nonlocal avatar state kept the player's original skin texture. Renderer model pointers returned to the vanilla player model after drawing, preventing a selected model from leaking into later renders.
- Real equipped sword, offhand shield and chestplate data stayed present. Held items rendered with the character. Native reported hitbox stayed 0.6 wide / 1.8 tall and eye height 1.62. Cosmetic armor/cape layers were replaced only on the custom local model, as designed.
- The separate PvP page still opened with eight categories after adding the ninth main-page category. At 640x480, all six character cards and nine sidebar rows remained accessible and native clicks worked.
- Saved Sandy, restarted the final Member JAR and confirmed the saved choice loaded and rendered without Premium. Tested exclusive On/Off again, inventory preview while geared and native Reset Astra preferences returning to the normal player. Inspected the rear model/tail geometry as well.
- The first sidebar-icon preview was cropped. Adjusted the authored icon's GUI transform, rebuilt both editions and inspected the corrected SpongeBob face in the final Member menu. Character geometry and other previews were unchanged.

The observer, synthetic gear commands, screenshots, runtime config and worlds do not ship. The game closed cleanly after both runs. Tests used Linux/software rendering, not Windows/GPU FPS benchmarking or a live authenticated DonutSMP server. These cosmetics are local and do not update the account skin or transmit a disguise to other players. Existing Windows/Defender limits remain in SECURITY.md and the limited-coverage scan report.
