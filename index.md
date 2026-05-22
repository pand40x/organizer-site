---
layout: default
title: Organizer
permalink: /
---

# Organizer

A private, local-first folder organizer for macOS.

Organizer watches the folders you pick, waits until files stop changing,
then queues moves for your approval. Nothing is sent off your Mac — no
analytics, no telemetry, no account, no network entitlements.

## Useful links

- **[Privacy policy](privacy/)** — what Organizer can and cannot see.
- **[Support](support/)** — how to ask a question or report a bug.

## What Organizer does

- Watches Downloads, Desktop, Documents, or any folder you grant.
- Sorts files by type and name patterns into clean category folders.
- Holds every suggested move for your review by default — **nothing
  moves until you approve it**.
- Optional clipboard history with sensitive-content filtering and
  Touch ID gate for hidden entries.

## What Organizer doesn't do

- It doesn't connect to the internet. The shipping App Store build
  has no `com.apple.security.network.client` or `network.server`
  entitlement, so the sandbox itself won't let it.
- It doesn't collect or transmit any data. The bundled privacy
  manifest declares zero collected data types and zero tracking.
- It doesn't ask for Full Disk Access. Organizer only sees folders
  you explicitly granted through the standard macOS open panel.
