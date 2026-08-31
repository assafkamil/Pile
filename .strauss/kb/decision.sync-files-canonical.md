---
type: decision
title: >-
  Sync treats the markdown files as canonical; whatever replicates, the files
  are the truth
description: >-
  Pile's identity is a journal you own as plain markdown - readable, greppable,
  portable without the app. Any sync design that demotes the files breaks that
  contract. Files-canonical also keeps the derived structures (index, tags,
  search) exactly what they are today: rebuilt locally per device, never synced.
  A conflict is a sibling file a human can open, not a database row a human
  cannot.
tags:
  - sync
  - architecture
generated:
  by: assafk
  at: '2026-08-31T19:55:47.436Z'
verified: []
strauss_anchors:
  - file: src/main/utils/pileHelper.js
  - file: src/main/utils/pileIndex.js
strauss_status: accepted
strauss_materiality: blocking
strauss_confidence: high
strauss_owner: assafk
---
## Decision

Sync treats the markdown files as canonical; whatever replicates, the files are the truth

## Rationale

Pile's identity is a journal you own as plain markdown - readable, greppable, portable without the app. Any sync design that demotes the files breaks that contract. Files-canonical also keeps the derived structures (index, tags, search) exactly what they are today: rebuilt locally per device, never synced. A conflict is a sibling file a human can open, not a database row a human cannot.

## Rejected

Database-primary (SQLite as truth, files as export) was rejected despite row-level merge and sync-engine ecosystem support: it trades away the app's identity for merge convenience and forces migration of every existing pile. A sync sidecar (synced oplog with per-entry versions and tombstones) was NOT rejected - it stays open as a possible merge aid subordinate to the files, to be decided when the merge mechanism is designed.

## Impact

Whole-file merge granularity is accepted; renames and deletes will need explicit handling; folder-syncer compatibility (Syncthing, iCloud Drive) becomes a design target rather than an accident. Every later sync decision is bounded by this one.

Relates to [fact.storage-model-markdown-on-disk](fact.storage-model-markdown-on-disk.md).
