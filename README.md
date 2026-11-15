# SigmaTools releases (public)

SigmaDesk's install and update files, read by the app through jsDelivr (GitHub raw as the backup).
Made with `sigmadesk-publish` (tools/publish in sigma-tools/sigmatools); nothing here is edited by hand.

| Path | What |
|---|---|
| `channels/windows-stable.json` | Signed (Ed25519) pointer: version, sequence, the exact commit, manifest hash, expiry |
| `packages/windows/<version>/manifest.json` | Every file of that version with size, SHA-256 and pieces |
| `chunks/sha256/<aa>/<sha256>.bin` | File pieces (gzip), named by the SHA-256 of their contents; shared between versions |
| `bootstrap/windows/<version>/sigmadesk.exe` | The program alone, for the node installer's first step |

Files are fetched at the commit the signed channel names, so a published version never changes.
Old commits are never rewritten; a release is withdrawn by publishing a newer signed channel.

Where the apps fetch these files from is set by the SigmaTools server's update guide
(`GET /v2/update/guide`, admin console → 업데이트); by default jsDelivr, then GitHub raw. The server
itself never sends these files. This repository replaces `sigma-tools/sigmadesk-releases`; the
channel's sequence continues from it (0.3.10 was 38), so installed apps accept the next release.
