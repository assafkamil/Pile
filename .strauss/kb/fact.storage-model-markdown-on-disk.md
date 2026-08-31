---
type: fact
title: >-
  Entries are per-pile markdown files on disk; index, tags, links and search are
  derived local structures; no sync, no accounts
description: >-
  Any multi-device sync design starts from what the current source of truth is.
  This pins it before the sync design session.
tags:
  - architecture
  - storage
  - pre-sync
sources:
  - id: source-read
    resource: 'Pile source at fork point, read 2026-08-31'
    author: assafk
generated:
  by: assafk
  at: '2026-08-31T05:53:12.225Z'
verified: []
strauss_anchors:
  - file: src/main/utils/pileIndex.js
  - file: src/main/utils/pileHelper.js
strauss_status: accepted
strauss_confidence: high
strauss_owner: assafk
---
## Claim

A pile is a directory; journal entries are markdown files inside it. The main process maintains derived structures over those files - an entry index, tags, links, and a search index - all local. There is no server, no account, and no sync mechanism of any kind.

## Evidence

Read from source at fork point (upstream dormant since Dec 2024): src/main/utils/pileIndex.js, pileTags.js, pileLinks.js, pileSearchIndex.js, pileHelper.js all operate on the local filesystem only.

## Implication

The sync design session must decide whether files on disk stay the source of truth (sync = file replication with merge) or a database becomes primary (files become an export). That choice, then CRDT versus server-authoritative merge, are the decisions to record when made.

[^source-read]: Pile source at fork point, read 2026-08-31
