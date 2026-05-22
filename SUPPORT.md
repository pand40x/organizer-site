---
layout: default
title: Support
permalink: /support/
---

# Organizer Support

We try to answer everything within a couple of business days.

## Contact

- **Email:** [anilsahin@yandex.com](mailto:anilsahin@yandex.com)

If you're reporting a bug, the following helps us reproduce it
quickly:

- macOS version (Apple menu → About This Mac)
- Organizer version (Settings → General → Version)
- Steps to reproduce
- What you expected vs. what happened
- A screenshot if anything looked wrong

Crash reports happen automatically through Apple's standard
mechanism if you opted in to share diagnostics with Apple — no
separate setup needed on our side.

## Frequently asked

**Does Organizer touch my files without asking?**
Not in the default Review mode. Files appear in a pending list
that you approve before anything moves. Auto mode is opt-in and
goes through a confirmation dialog the first time you enable it.

**Can I undo a move?**
Yes. Every move shows up under Dashboard → Recent moves and
Activity → Moves with a hover-revealed Undo button.

**How do I delete my clipboard history?**
Settings → Clipboard → Maintenance → Delete clipboard history.
This deletes both the JSON entries and the encrypted image
blobs in your local Application Support folder.

**Does Organizer support Intel Macs?**
Yes. The shipped binary is universal (arm64 + x86_64) and the
minimum OS is macOS 14.

**Where is my data stored?**

```text
~/Library/Containers/app.organizer.macos/Data/Library/Application Support/Organizer/
```

You can inspect, back up, or wipe this folder freely — Organizer
recreates the files it needs on the next launch.

## Privacy

See the [privacy policy](/organizer-site/privacy/) for what
Organizer does and does not handle.
