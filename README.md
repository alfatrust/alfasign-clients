# alfasign-clients

Update feeds for the AlfaSign desktop apps, served by GitHub Pages at
**https://apps.alfasign.ro** (custom domain — see `CNAME`, which GitHub manages;
don't delete it).

| Path | Consumer | Published by |
|---|---|---|
| `windows/appcast.xml` (+ `.signature`) | AlfaSign for Windows, x64 (NetSparkle) | AlfaSignWindows GitLab CI on `win-v*` tags |
| `windows/appcast-arm64.xml` (+ `.signature`) | AlfaSign for Windows, ARM64 | same |
| `windows/token/appcast.xml` (+ `.signature`) | Reînnoire certificat AlfaSign (token app, portable exe; NetSparkle) | ReinnoireOnline GitLab CI on `win-token-v*` tags |
| `windows/token/test/appcast.xml` (+ `.signature`) | same, test channel | same, on `win-token-test-v*` tags (pre-releases) |
| `macos/appcast.xml` | AlfaSign for macOS (Sparkle) | macOS release pipeline on `mac-v*` tags |

Installers are attached to this repo's GitHub Releases: `win-v<version>` for
Windows, `mac-v<version>` for macOS. The token app's exe is attached to
`win-token-v<version>` (and `win-token-test-v<version>`, a pre-release).
`windows/token/` belongs to the token app's pipeline, not AlfaSign for Windows'.

## Rules

- **Paths are a public contract.** The feed URLs are compiled into every
  installed app; renaming a folder or file strands the installed base.
- **Each pipeline writes only its own folder.** Never commit to another
  platform's folder.
- **Don't edit appcasts by hand.** Each is Ed25519-signed; the apps reject a
  feed or download whose signature doesn't verify.
- **Always link `https://apps.alfasign.ro/...`, never `alfatrust.github.io`.**
  The custom domain is what lets the feed move hosts with a DNS change only.
  It's a Cloudflare CNAME → `alfatrust.github.io`, DNS only (grey cloud) so
  GitHub can issue its certificate.
