# Astra 1.27.0 owner setup — JackJ25

Premium exports are assigned to a Java account before sharing. They expire 30 days after issuance. No Astra server is installed or required.

## Install the private owner setup

1. Install one Astra 1.27.0 release JAR and Fabric API in your Minecraft instance's `mods` folder. The Member JAR can issue files too. The owner Premium download is already bound to JackJ25.
2. Download the **private owner setup ZIP supplied directly in the conversation**. It is deliberately not hosted in the public GitHub repository.
3. Extract it into the same Minecraft instance folder that contains `mods` and `config`. The resulting key path must be `config/astra-owner/issuer.pk8`.
4. Sign in with your Minecraft Java account **JackJ25**. Join a world and type `/client <username>` in chat. For example: `/client JackJ25`.
5. Wait for the confirmation. The newly created JAR is in the instance's `astra-premium-exports` folder. Send **only that recipient's JAR**. They remove their old Astra JAR and install this one alongside Fabric API.
6. To give the same player a fresh 30 days, run `/client <their current Java username>` again and send the newly generated file. Each file has its own signed serial and expiration; their previous file is not rewritten or revoked.

The key must match the public verification key bundled in this release. A missing or wrong key gives an error and does not create an export. A different launcher account cannot use the owner command in the unchanged client, even if it uses the same display name. The command is local to Astra; it is not sent as a DonutSMP server command.

## Keep the issuing key private

Never send the owner ZIP, `issuer.pk8`, your complete config folder or a backup containing it to a Premium recipient. Never commit them to GitHub or include them in a public mod pack. Keep a private backup: without the matching key, new licenses cannot be issued for this public verifier. If the key is exposed, replacing the trust key requires rebuilding/updating clients; an offline system cannot centrally revoke old files.

The owner command reads the key only to sign a grant. The exported JAR includes that signed grant and the **public** verifier, not the private key. Public source/build tools contain no private issuer key. Ed25519 signs license metadata; this is not a Microsoft Authenticode or JAR certificate-signing claim.

## What the restriction does

An unchanged client checks the launcher's Minecraft UUID against the signed recipient UUID. Renaming an account keeps its UUID and access. Passing the file to another normal signed-in account keeps that account in Member mode. A changed or invalid grant also uses Member mode. The old resettable local timer is not accepted as a license. The Profile page shows the licensed name, fixed expiry and remaining time.

This is an offline restriction, not an unbreakable DRM service. It cannot globally claim a file on first launch, verify arbitrary offline/custom-launcher identity spoofing, stop modified clients, provide a trusted clock, revoke existing copies or invalidate older Astra versions. The same licensed account can use its file on another computer until expiration. A signed-in account owns the file before launch; there is no anonymous first-user claim step.

`/client` uses a background HTTPS request to Microsoft's official `api.minecraftservices.com/minecraft/profile/lookup/name/<username>` endpoint to resolve the recipient. It sends only the requested public username; no access token or issuer key is sent. Internet is needed to issue a new file. Normal offline license checks do not contact Astra or a licensing server.

The 3D Characters Work In Progress lock applies to both editions until 15 December 2026, independently of Premium. Its date/progress also follows the device clock.
