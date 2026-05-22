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

Everything stays on the device. No analytics, no telemetry, no
account, and no network entitlements at all — the shipping
sandbox simply doesn't allow it.

- **[Privacy policy](privacy/)** — what Organizer can and cannot see.
- **[Support](support/)** — how to ask a question or report a bug.

---

## File Organizer

Pick the folders you want to keep tidy. Organizer watches them
in the background and surfaces suggested moves whenever new
files settle.

- **Watch any folder** — Downloads, Desktop, Documents, or any
  user-selected directory.
- **Per-folder wait window** — wait 1 minute to 2 hours after the
  file last changed before suggesting a move.
- **Four explicit modes** — Review (default), Auto, Preview,
  Manual. Auto is opt-in and the first switch goes through a
  confirmation dialog.
- **Smart classifier** — extension + name heuristics + your own
  rules slot files into Images, Documents, Code, Archives,
  Screenshots, Installers, and more.
- **Safe moves only** — never overwrites, never deletes; name
  collisions get a " (2)" suffix; hidden files, symlinks, app
  bundles, package directories, and iCloud placeholders are
  always skipped.
- **Reversible** — every move appears in Recent Moves with a
  hover-revealed Undo button.
- **Per-move audit journal** — wrapped in a durable transaction
  so a crash mid-move never leaves files in limbo.

## Clipboard

An opt-in clipboard manager that holds onto what you copied so
nothing important gets buried under the next paste — but treats
the clipboard with the privacy it deserves.

- **Off by default** — turn it on in Settings → Clipboard
  whenever you want it; nothing is recorded until you do.
- **Three privacy postures**, switchable from Settings and from
  the menubar popover:
  - **Visible** — clips render normally.
  - **Hidden** — previews are masked behind dots; click to
    reveal for five seconds.
  - **Locked** — same as Hidden, but every reveal goes through
    Touch ID or the system password.
- **Encrypted at rest** — clipboard entries and image clips are
  written as AES-256-GCM ciphertext. The symmetric key lives in
  the local keychain and never syncs to iCloud. If the keychain
  is unavailable when a clip would otherwise be saved, the clip
  is discarded rather than written in plaintext.
- **Sensitive content filtered** — clipboards that apps mark as
  private (password managers, one-time codes) are skipped. So
  are strings that look like API tokens, private keys, or JWTs.
- **Pause without unchecking** — one-tap pause for sessions
  where you're handling secrets you don't want recorded.
- **Pin, edit, delete** — keep important clips around, edit
  text in place, drop the rest in one click.

## App

- **Menubar app** — quick stats, top three pending moves, and an
  "Organize now" button. Open the full window only when you
  want to.
- **First-run onboarding** — pick the folders to watch, grant
  permissions through the standard macOS open panel, opt into
  clipboard if you want it.
- **Universal binary** — runs natively on Apple Silicon and
  Intel Macs; minimum macOS 14.
- **Sandboxed** — App Sandbox + user-selected folder access +
  per-folder security-scoped bookmarks. No Full Disk Access.

---

## What Organizer doesn't do

- It doesn't connect to the internet. The shipping App Store
  build has no `com.apple.security.network.client` or
  `network.server` entitlement, so the sandbox itself won't let
  it.
- It doesn't collect or transmit any data. The bundled privacy
  manifest declares zero collected data types and zero
  tracking.
- It doesn't ask for Full Disk Access. Organizer only sees
  folders you explicitly granted.
- It doesn't sell anything. Free, no in-app purchases, no
  subscriptions, no ads.
