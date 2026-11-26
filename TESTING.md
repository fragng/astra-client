# Astra Client1.34.0 validation

- Java21 / Minecraft1.21.11 / Fabric Loader0.19.3 Member and Premium-template builds pass26 required tasks. Existing browser input, Windows media ABI, Wordle, cases, licensing, mesh and other contracts remain required.
- New UiPerformanceTest verifies frame-rate-independent settling at 20/60/144 fps, dropped-frame recovery, motion-off behavior, bounded text reuse, normal/heading separation, long-text bypass, gradient quad/bounds/clipping invariants, transparent rounded corners and single-layer alpha coverage.
- CaseSpinTest exercises800 committed outcomes and192,800 reel frames. Essential motion advances without any decorative animation/performance parameter. Centre-marker landing, monotonic motion, duration, resume and committed outcome remain consistent. Existing case distribution/allowance/claims contracts pass.

## Native baseline and updated menu

The same local Fabric observer measured ScreenEvents before/after render and counted non-text GuiRenderState elements before glyph expansion. It is outside the source/release. Both runs used Minecraft's1280×720 window, GUI640×360/scale2, the Visuals page, Bubble Font and Linux software OpenGL. World rendering remained active. This is a diagnostic comparison, not a controlled whole-game FPS benchmark.

| Measure |1.33.1 baseline|1.34.0|
|---|---:|---:|
|Median non-text GUI elements/frame|5,643|1,047|
|Median UI submission CPU time|24.65ms|8.78ms|
|Samples in12-second capture|48|25|

The new capture contained24 batched gradient elements/frame. Submission count fell81.4%; the sampled UI CPU median fell64.4%. Hardware/software driver scheduling, world work and capture sample counts differ; these numbers do not establish a whole-game FPS gain. No fixed FPS claim is made.

Native checks:

- Baseline1.33.1 reproduced the static reel with Smooth animations Off: the visible position range was0.0 during the timed opening.
- Updated real OPEN actions moved the reel by27.66 cards in normal mode,27.86 with decorative animations off, and25.86 with animations off plus Performance Mode. Each retained one new committed draw through landing and used the correct allowance behavior. This pre-existing test account had Infinite Cases, so its allowance appropriately stayed unchanged. Reward/allowance rules were not modified for testing.
- Actual FOV and brightness slider clicks updated their settings and restored the original FOV after close/reopen. Black/Blue/Red/Pink/Purple switched correctly, Bubble Font and Minecraft font were inspected, and every sidebar page opened.
- Screenshots confirmed rounded gradients, colours, labels and clipping. The640×480 window and menu close/reopen also passed. The test driver was corrected to include the window's screen position after Minecraft recentered a resize; application behavior required no workaround.
- Performance Mode applied6-chunk rendering/5-chunk simulation in the run, then restored12/8 when disabled. Case motion continued in both states. Minecraft exited successfully and saved the world.

## Retained limits

Live Windows performance/Spotify/browser behavior is not tested on this Linux host. Krillion's browser-input and once-only shutdown repairs are retained; the actual website still encounters the cloud proxy's TLS trust issue, and no certificate bypass is used. Its controls were previously tested in a real CEF local resource fixture;1.34.0 changes only the shared GUI labels used in that screen.

Archive checks verify unchanged dependency hashes/assets/backend rules, matching edition code, original signed owner grant/expiry and absence of private keys or native observers. See the versioned scan report for the final artifact scope and results. The earlier Windows antivirus warning remains unresolved; keep any protection block in place.
