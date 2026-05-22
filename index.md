---
layout: default
title: Organizer
permalink: /
---

# Organizer

A private, local-first companion app for your Mac. Two features
in one: a folder organizer that tidies Downloads / Desktop /
Documents on your approval, and a clipboard manager that
remembers what you copied without ever leaving your Mac.

- **[Privacy policy](privacy/)** — the legal document for App
  Store Connect.
- **[Support](support/)** — contact email and bug-report tips.

---

## Privacy & Security

Organizer's privacy guarantees are not marketing copy — they
are enforced by the macOS sandbox itself, by the bundled
privacy manifest, and by code paths that fail closed instead
of degrading silently.

### Network: there is none

The Mac App Store build ships with neither
`com.apple.security.network.client` nor
`com.apple.security.network.server` entitlements. App Sandbox
denies every outbound connection at the kernel level — even
if a bug or a future dependency tried to phone home, it
physically cannot. The release script refuses to sign a bundle
whose entitlements grew either key, so this stays true across
updates.

No analytics SDK, no advertising SDK, no telemetry uploader,
no remote API client, no crash reporter, no auto-updater. The
`Package.swift` declares zero third-party dependencies; the
binary links only Apple frameworks (AppKit, SwiftUI, FSEvents,
LocalAuthentication, CryptoKit).

### Storage: yours, on your Mac

All data Organizer keeps lives under:

```text
~/Library/Containers/app.organizer.macos/Data/Library/Application Support/Organizer/
```

You can inspect, back up, or wipe that folder freely. There is
no separate cloud, no separate database, no opaque container.
Settings, history, and bookmarks are plain JSON. Clipboard
entries and image clips are AES-256-GCM ciphertext.

### Encryption at rest for the clipboard

Clipboard entries and image blobs are encrypted with
**AES-256-GCM** before they touch the disk. The symmetric key
is generated on first use, stored in the **local keychain
only** (`kSecAttrSynchronizable = false`), and accessible
whenever you're logged in.

What this protects you from:

- **Time Machine and unencrypted backups** — without the
  keychain entry, the backed-up files are random bytes.
- **A FileVault-off Mac whose disk is removed** — the files
  are accessible but unreadable without the keychain.

What encryption alone cannot protect:

- Someone using your unlocked, logged-in Mac. The keychain
  is unlocked and the app can read the key, exactly like
  every other Mac app. The separate **Locked clipboard mode**
  exists for that threat: it gates every reveal behind Touch
  ID or the system password.

If the keychain is unavailable when a clip would otherwise be
saved — keychain corruption, profile errors, edge cases —
the clip is **discarded** rather than written in plaintext.
The encryption promise is fail-closed.

### Sandboxed folder access

Organizer uses standard macOS **App Sandbox** with two
narrow entitlements:

- `com.apple.security.app-sandbox`
- `com.apple.security.files.user-selected.read-write`
- `com.apple.security.files.bookmarks.app-scope`

That's the full list. **Full Disk Access is never requested.**
Each watched folder is granted by you through the standard
macOS open panel, then remembered across launches via
security-scoped bookmarks. The folder picker explicitly
rejects system paths (`/`, `/System`, `/Library`, `/private`,
`/usr`, `/bin`, `/sbin`, `/cores`, `/Volumes`,
`/Applications`) so an accidental selection can't drag the
app into protected territory.

### Privacy manifest

The bundled `PrivacyInfo.xcprivacy` declares:

- `NSPrivacyCollectedDataTypes`: **empty array** (no data
  collected).
- `NSPrivacyTracking`: **false**.
- `NSPrivacyTrackingDomains`: **empty array**.
- Required-reason APIs are declared honestly:
  - `NSPrivacyAccessedAPICategoryFileTimestamp` with reasons
    `3B52.1` (access metadata on user-granted folders) and
    `DDA9.1` (display modification dates in the UI).
  - `NSPrivacyAccessedAPICategoryUserDefaults` with reason
    `CA92.1` (persist this app's own preferences).

### Sensitive-content filter for the clipboard

Before any clip is recorded, Organizer runs three checks:

1. **Concealed-clipboard convention** — clipboards marked
   with `org.nspasteboard.ConcealedType` (1Password,
   Bitwarden, the system one-time-code surface) are skipped.
2. **Token-shape heuristics** — strings that match common
   secret patterns (API tokens like `sk-…` / `ghp_…` /
   `xox[bpoa]-…`, AWS access keys, Stripe live secret keys,
   JWTs, PEM-encoded private keys) never land in history.
3. **High-entropy single-word** — long, mixed-case,
   high-digit-density strings are treated as probable
   secrets.

Anything flagged is reported in the activity log without the
content — the activity feed itself never carries clipboard
text.

### Move safety

Files are only moved after they've stopped changing for your
configured wait window. The actual move:

- **Never deletes the source** — only `FileManager.moveItem`
  (or `replaceItem` / `trashItem` if you explicitly chose
  Overwrite). The original is gone only on a successful move.
- **Never overwrites by default** — name collisions become
  `foo (2).pdf`, never destructive.
- **Skips protected items** — hidden files, symlinks, app
  bundles, package directories (`.photoslibrary`, `.rtfd`),
  alias files, and iCloud `.icloud` placeholders are never
  touched.
- **Is journaled** — every move is wrapped in a write-ahead
  log on disk. If the app crashes mid-move, the next launch
  recovers a consistent state and surfaces the audit entry.
- **Is reversible** — every move shows up in Recent Moves
  with a hover-revealed Undo button that puts the file back
  exactly where it came from.

---

## File Organizer

Pick the folders you want to keep tidy. Organizer watches them
in the background and surfaces suggested moves whenever new
files settle.

- **Watch any folder** — Downloads, Desktop, Documents, or any
  user-selected directory.
- **Per-folder wait window** — wait 1 minute to 2 hours after
  the file last changed before suggesting a move.
- **Four explicit modes** — Review (default), Auto, Preview,
  Manual. Auto is opt-in; the first switch goes through a
  confirmation dialog.
- **Smart classifier** — extension + name heuristics + your
  own rules slot files into Images, Documents, Code, Archives,
  Screenshots, Installers, and more.
- **Per-move audit journal** — wrapped in a durable
  transaction so a crash mid-move never leaves files in limbo.
- **Reversible** — every move appears in Recent Moves with a
  hover-revealed Undo button.

## Clipboard

An opt-in clipboard manager that holds onto what you copied so
nothing important gets buried under the next paste — but
treats the clipboard with the privacy it deserves.

- **Off by default** — turn it on in Settings → Clipboard
  whenever you want it; nothing is recorded until you do.
- **Three privacy postures**, switchable from Settings and
  from the menubar popover:
  - **Visible** — clips render normally.
  - **Hidden** — previews are masked behind dots; click to
    reveal for five seconds.
  - **Locked** — same as Hidden, but every reveal goes
    through Touch ID or the system password.
- **Encrypted at rest** — see the Privacy & Security section
  above.
- **Pause without unchecking** — one-tap pause for sessions
  where you're handling secrets you don't want recorded.
- **Pin, edit, delete** — keep important clips around, edit
  text in place, drop the rest in one click.
- **Image clips opt-in** — clipboard image capture is
  disabled by default; turning it on writes the same AES-GCM
  ciphertext to disk.

## App

- **Menubar app** — quick stats, top three pending moves, and
  an "Organize now" button. Open the full window only when
  you want to.
- **First-run onboarding** — pick the folders to watch, grant
  permissions through the standard macOS open panel, opt into
  clipboard if you want it.
- **Universal binary** — runs natively on Apple Silicon and
  Intel Macs; minimum macOS 14.
- **Free, no purchases** — no in-app purchases, no
  subscriptions, no ads.
