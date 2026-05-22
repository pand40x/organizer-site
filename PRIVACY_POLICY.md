---
layout: default
title: Privacy Policy
permalink: /privacy/
---

# Organizer Privacy Policy

Organizer is a local-first macOS utility. The app does not collect, transmit,
sell, rent, or share personal data.

## Data Organizer Handles

Organizer can process:

- folder paths selected by the user;
- file names, file sizes, file dates, and file locations needed to suggest or
  perform organization;
- local move history so the user can review or undo moves;
- optional clipboard history when the Clipboard module is explicitly enabled.

This data stays on the user's Mac under:

```text
~/Library/Containers/app.organizer.macos/Data/Library/Application Support/Organizer/
```

Clipboard history and image clips are stored as AES-256-GCM ciphertext. The
symmetric key lives in the local keychain (no iCloud sync). If the keychain
is unavailable when a clip would otherwise be saved, the clip is discarded
rather than written in plaintext.

## Network and Tracking

Organizer has no analytics SDK, advertising SDK, telemetry upload, account
system, or remote API client. Its Mac App Store entitlements intentionally omit
network client and server permissions.

Organizer does not track users across apps or websites.

## Clipboard

Clipboard History is disabled by default. If enabled, likely-sensitive content
is skipped by default, image capture is disabled by default, and persistence
across launches is disabled by default. Users can delete local clipboard history
from **Settings → Clipboard → Maintenance**.

## Folder Permissions

Organizer uses macOS App Sandbox and user-selected folder access. Security-scoped
bookmarks let the app remember selected folders across launches without Full Disk
Access.

## Deleting Local Data

Users can clear clipboard history from **Settings → Clipboard → Maintenance**
and clear file-organizer move history from **Settings → File Organizer →
Maintenance**. They can also remove Organizer's local storage folder from:

```text
~/Library/Containers/app.organizer.macos/Data/Library/Application Support/Organizer/
```

## Contact

Questions, requests, and bug reports about Organizer or this privacy policy:

- Email: <anilsahin@yandex.com>
- Support page: <https://pand40x.github.io/organizer-site/support/>

Last updated: 2026-05-22.
