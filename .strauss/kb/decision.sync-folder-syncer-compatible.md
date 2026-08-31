---
type: decision
title: Sync transport is delegated to folder syncers; Pile's job is surviving them
description: >-
  With files canonical, a third-party folder syncer (Syncthing, iCloud Drive)
  already moves the bytes. Pile writes zero transport code and instead becomes
  safe under external syncing: atomic entry writes so a syncer never ships a
  half-written file, detection and surfacing of syncer conflict copies in the
  UI, and index/tags/search rebuild resilience when files change underneath the
  app. This keeps the no-accounts identity intact and makes sync available the
  day conflict-safety lands, not the day a server ships.
tags:
  - sync
  - architecture
generated:
  by: assafk
  at: '2026-08-31T19:59:49.782Z'
verified: []
strauss_anchors:
  - file: src/main/utils/pileHelper.js
  - file: src/main/utils/pileIndex.js
strauss_verify:
  - >-
    Before implementation: reproduce a Syncthing conflict copy on a real pile
    and confirm the planned detection surface catches it.
strauss_status: accepted
strauss_materiality: blocking
strauss_confidence: medium
strauss_owner: assafk
---
## Decision

Sync transport is delegated to folder syncers; Pile's job is surviving them

## Rationale

With files canonical, a third-party folder syncer (Syncthing, iCloud Drive) already moves the bytes. Pile writes zero transport code and instead becomes safe under external syncing: atomic entry writes so a syncer never ships a half-written file, detection and surfacing of syncer conflict copies in the UI, and index/tags/search rebuild resilience when files change underneath the app. This keeps the no-accounts identity intact and makes sync available the day conflict-safety lands, not the day a server ships.

## Rejected

An owned relay server was rejected for now: it buys merge control and a mobile path at the price of accounts, infrastructure, and an E2E-encryption question - a second identity fight immediately after settling the first. Peer-to-peer was rejected as real pairing/discovery complexity without the control a relay would at least buy. Both remain plausible futures; this decision is the one most likely to be revisited if conflict-copy UX proves insufficient in practice.

## Impact

The sync milestone becomes conflict-safety work inside the app rather than infrastructure: atomic writes, conflict-copy handling, rebuild robustness. No server costs, no accounts. Sync timing and delivery semantics are ceded to the third-party syncer.

Relates to [decision.sync-files-canonical](decision.sync-files-canonical.md).
