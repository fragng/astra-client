# Third-party components in Astra 1.34.0

## CreamyKeys — user-provided original

Author: cutebow. Exact uploaded CreamyKeys Universal 0.0.5, SHA-256 `023767afb373dcf16f0e0768d358e253fc072ebd3719d7609772c8057d094730`, is included byte-for-byte in `libs/creamykeys-universal-0.0.5.jar` and nested in the release. Its metadata declares All Rights Reserved; this package does not relicense it. The universal wrapper contains its original compatible CreamyKeys 0.0.5 implementation and JLayer 1.0.1. Original metadata, notices and licenses are preserved inside those JARs. The uploader is responsible for permission to redistribute their supplied dependency. There is no additional Astra Creamy Keys engine. Settings are owned by that original mod.

## MCEF Modern / JCEF

[MCEF Modern](https://github.com/Dimaskama/mcef-modern), version0.3.3 for Minecraft1.21.11 / JCEF146.0.10, LGPL-2.1. Original JAR SHA-256 `5d7b0da06c97085fde4f76bc1b98fe2765a270a006dd8b37d903bd479eb27dda`. Astra uses the unchanged SDK and applies its own security/shutdown mixins, an idempotent JCEF termination guard and a local browser subclass for input compatibility and bounded frame staging/upload. These additions are included in Astra source.

Corresponding MCEF Modern, jcefmaven and JCEF API source archives and the LGPL text are in `third-party/mcef-modern/` in the complete source ZIP. Original licenses remain inside the dependencies. You may replace or rebuild these LGPL components for your own use, subject to compatibility; the source project's `libs` and `libs/browser-api` inputs make their versions explicit. Preserve third-party notices on redistribution. No private key is needed to build the Member client.

Native JCEF/CEF components are downloaded by MCEF on first Krillion use and cached in the instance's `config/mcef-modern/jcef` directory, subject to upstream platform layout. They are not in the Astra download. Retain the upstream CEF/Chromium third-party notices shipped with that runtime. Browser helper processes and additional disk usage are expected. Only the supplied Krillion page is exposed; this is not a general browser or a Minecraft scripting bridge. The site and its assets remain their owners' work; the game is loaded live rather than copied/relicensed. Browser TLS checks remain enabled.

## Freelook and voices

Freelook1.2.8 remains the exact original bundled dependency; source/notices are in `third-party/freelook/`. Existing character-audio licensing is documented in [CHARACTER_VOICES.md](CHARACTER_VOICES.md). These components are unchanged in this preview.
