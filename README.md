# Bizzy releases

Download page for the **Bizzy desktop app** (macOS, Apple silicon). This repo
has no source code. It holds the release files, and the app checks it for
updates.

## Install

1. Open the [latest release](https://github.com/33Audits/bizzy-releases/releases/latest).
   Preview builds are under [all releases](https://github.com/33Audits/bizzy-releases/releases).
2. Download `Bizzy-<version>-mac-arm64.dmg`.
3. Open the DMG and drag **Bizzy** onto **Applications**.
4. The first launch needs one extra step because Bizzy is not yet signed with an
   Apple Developer ID:
   - In Finder, open **Applications**, **right-click Bizzy → Open**, then
     choose **Open** in the dialog. Or:
   - If macOS says Bizzy "can't be opened", go to **System Settings → Privacy &
     Security**, scroll to Security, and click **Open Anyway**. Or:
   - In Terminal, run `xattr -dr com.apple.quarantine /Applications/Bizzy.app`
     and then open Bizzy normally.

After that, Bizzy opens like any other app.

## Updates

Bizzy checks this repo when it starts and every 6 hours. You can also use
**Bizzy → Check for Updates…** or the **About** section in Settings. When a new
version is out you'll see "Update available". Click **Download**, and then
**Restart to update** when it's ready. If you quit instead, the update is
installed on the way out.

Before installing, the app checks the download's size and SHA-256 against the
release's `latest-mac.json`, and checks that the unpacked app is Bizzy at the
expected version. If anything fails, the update isn't installed. If the new
version doesn't start, your previous version is put back.

Preview builds only get preview updates. A regular build gets them only if you
turn on **Preview releases** in Settings.

## Verify a download

Every release includes `SHA256SUMS.txt`. In the folder where you downloaded the
files:

```sh
shasum -a 256 -c SHA256SUMS.txt --ignore-missing
```

Each file you downloaded should be reported as `OK`. You can also compare one
file by hand:

```sh
shasum -a 256 Bizzy-<version>-mac-arm64.dmg
```

The hash should match the line for that file in `SHA256SUMS.txt` and in the
release notes.

## What's in a release

| Asset | Purpose |
| --- | --- |
| `Bizzy-<version>-mac-arm64.dmg` | Installer: drag to Applications |
| `Bizzy-<version>-mac-arm64.zip` | The app as a zip; this is what in-app updates download |
| `SHA256SUMS.txt` | SHA-256 for the DMG and the zip |
| `latest-mac.json` | Update manifest the app reads (version, notes, zip/dmg URL, SHA-256, size) |

Releases are tagged `vX.Y.Z`. Versions with a suffix, like `v0.18.0-preview.1`,
are marked as pre-releases.

- **Stable feed:** `https://github.com/33Audits/bizzy-releases/releases/latest/download/latest-mac.json`
  (GitHub's "latest release", which never points to a pre-release)
- **Preview feed:** `channels/preview/latest-mac.json` in this repo, which
  always points to the newest release of either kind

Releases are published by the Bizzy team's release script
(`apps/desktop/scripts/release-bizzy.mjs`). Please don't upload files by hand.
