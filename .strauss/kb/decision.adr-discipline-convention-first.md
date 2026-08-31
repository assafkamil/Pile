---
type: decision
title: >-
  Decision capture wired as CLAUDE.md convention at three integration points; no
  mechanical gate for now
description: >-
  Decision records enter the workflow where the context exists: load the bundle
  before design, write a decision or an explicit no-decision at every subtask
  finalize, read records during review with same-cycle supersession. Wiring this
  as repo convention (CLAUDE.md) costs nothing and starts capture immediately;
  the machinery (kb_* tools, recording-decisions selectivity skill) is already
  available to every session on this machine.
tags:
  - workflow
  - adr-discipline
generated:
  by: assafk
  at: '2026-08-31T06:59:56.615Z'
verified: []
strauss_status: accepted
strauss_materiality: important
strauss_confidence: medium
strauss_owner: assafk
---
## Decision

Decision capture wired as CLAUDE.md convention at three integration points; no mechanical gate for now

## Rationale

Decision records enter the workflow where the context exists: load the bundle before design, write a decision or an explicit no-decision at every subtask finalize, read records during review with same-cycle supersession. Wiring this as repo convention (CLAUDE.md) costs nothing and starts capture immediately; the machinery (kb_* tools, recording-decisions selectivity skill) is already available to every session on this machine.

## Rejected

A mechanical why-gate (a hook that blocks ending a turn or committing until a decision or no-decision is recorded) was deferred, not rejected on principle: building enforcement for this fork right now is speculative tooling ahead of need, and pretending convention is enforcement is the failure mode documented in the ecosystem. If capture silently drops in practice - subtasks finishing with neither record nor no-decision call - that is the trigger to build the gate.

## Impact

Every future session in this repo loads the bundle first and pays capture cost at the moment of choice. The honest status (convention, not enforcement) is stated in CLAUDE.md itself.

Relates to [fact.storage-model-markdown-on-disk](fact.storage-model-markdown-on-disk.md).
