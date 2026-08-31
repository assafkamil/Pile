---
type: open-question
title: >-
  When the same entry is edited on two devices before syncing, what does the
  user see?
description: >-
  Folder syncers produce conflict copies at file granularity; whether Pile
  resolves them, merges them, or presents both is undecided and shapes the
  conflict-safety work.
tags:
  - sync
  - conflicts
generated:
  by: assafk
  at: '2026-08-31T19:59:49.990Z'
verified: []
strauss_status: open
strauss_owner: assafk
---
## Question

Same entry edited on two devices in the offline window: does Pile auto-merge text (CRDT/three-way), pick a winner (last-write-wins) and keep the loser as a sibling, or present both versions and let the user resolve?

## Why it matters

This is the whole user-facing surface of sync conflicts. Auto-merge risks silent garbling of journal prose; LWW risks silent loss without a visible sibling; manual resolution costs attention on every conflict.

## Default assumption

Per-entry last-write-wins with the losing version kept as a visible sibling entry the user can open and merge by hand. Rationale: journaling is single-author multi-device, concurrent same-entry edits are rare, and a visible sibling is the honest failure mode. CRDT text merge is deferred until real conflict frequency is observed.

Relates to [decision.sync-folder-syncer-compatible](decision.sync-folder-syncer-compatible.md).

Relates to [decision.sync-files-canonical](decision.sync-files-canonical.md).
