# Astra Client 1.22.0 validation

## Build and geometry checks

- Built Member and 30-day Premium for Java 21 / Minecraft 1.21.11 / Fabric Loader 0.19.3. Existing native Windows media ABI and six-theme transition/layout tests passed, alongside the new curved-surface contract tests.
- Curved-surface tests cover softened boxes, ellipsoids, both taper directions and the helmet ring. They verify finite vertices, unit normals, nondegenerate triangles, outward winding, positive enclosed volume, three-dimensional bounds and truly round silhouettes with radial lighting normals.
- The original authoring generator now defines 193 rounded primitives across the same six characters and a 39-colour 512x512 atlas. SpongeBob keeps softened square proportions; Patrick's stepped head/belly are replaced with tapered/round forms, DrDonutt has rounded hair/facial features, Squidward has smooth bulbs/tentacles, Mr. Krabs has round pincers and Sandy has a transparent bubble helmet and curved tail.
- Surfaces are generated once and cached; a ModelPart.Cube subclass emits the cached vertices through Minecraft's existing vertex API. Native world models and skin previews share geometry with independent articulated pose instances. Source definitions, generator and tests are included.
- Archive integrity passed, with identical code/assets between editions except version/edition metadata. Only character surface/preview class families changed from 1.21.0. Menu/config/render-guard classes, original Jamble, PvP, background travel and media code remain byte-identical. Removed Jamble payment/review classes stay absent. No runtime scripts, executables or excluded test fixtures ship.
- Original nested Freelook SHA-256 remains fe1a32d9e4b8894122f52985c9d81b5cefa7bb7b67e67d17e8d03c495f8ba1e4.

## Actual packaged Minecraft checks

Ran packaged Premium and the final Member edition with excluded observation helpers in a local creative world:

- Native clicks selected all six characters one at a time; each actual F5 model used the curved geometry. The six menu previews rendered the same refined models through Minecraft's native skin-preview renderer. The small SpongeBob sidebar icon remained visible.
- Native model checks confirmed 3D extents, actual walk-animation leg poses and cached model reuse. Inventory rendering and matching empty-hand first-person SpongeBob/Mr. Krabs hands worked. The selected switch Off restored the normal player and texture.
- Local render states selected the character atlas; a separate nonlocal avatar retained the original skin. The renderer returned to its normal model after drawing. Actual sword, offhand shield and chestplate data remained present; held items rendered. Native hitbox stayed 0.6 wide / 1.8 tall and eye height 1.62.
- Nine main-page categories, the separate eight-category PvP page, all six character cards and native toggle clicks remained accessible at 1280x720 and 640x480. Inspected the curved previews at both sizes.
- Saved Sandy and restarted the final Member edition. Confirmed the saved choice loaded without Premium, toggles and Off still worked, the native geared inventory preview rendered and Reset Astra preferences restored the normal player. Inspected the rear model/tail and closed the game cleanly.

Observer code, synthetic gear commands, screenshots, runtime preferences and worlds do not ship. Tests used Linux/software rendering; no Windows/GPU FPS benchmark or live authenticated DonutSMP server was available. These are local cosmetics, without account-skin changes or a transmitted disguise. Windows/Defender limits remain in SECURITY.md and the limited-coverage scan report.
