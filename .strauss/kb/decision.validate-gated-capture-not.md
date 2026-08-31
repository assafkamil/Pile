---
type: decision
title: >-
  KB integrity is gated mechanically at push; decision capture deliberately is
  not
description: >-
  A pre-push hook (.githooks/pre-push, wired via core.hooksPath) blocks any push
  while strauss-kb validate reports broken cross-record pointers. Integrity is
  gated because it is mechanically checkable with zero false positives: a
  dangling supersession pointer is always a defect, so a hard gate costs
  nothing. The hook skips with a warning when the CLI is absent, so
  upstream-style contributors without the tool are not blocked.
tags:
  - workflow
  - adr-discipline
  - enforcement
generated:
  by: assafk
  at: '2026-08-31T16:22:38.334Z'
verified: []
strauss_anchors:
  - file: .githooks/pre-push
  - file: CLAUDE.md
strauss_status: accepted
strauss_materiality: non-blocking
strauss_confidence: high
strauss_owner: assafk
---
## Decision

KB integrity is gated mechanically at push; decision capture deliberately is not

## Rationale

A pre-push hook (.githooks/pre-push, wired via core.hooksPath) blocks any push while strauss-kb validate reports broken cross-record pointers. Integrity is gated because it is mechanically checkable with zero false positives: a dangling supersession pointer is always a defect, so a hard gate costs nothing. The hook skips with a warning when the CLI is absent, so upstream-style contributors without the tool are not blocked.

## Rejected

Gating capture the same way (block a push or turn until a decision or no-decision is recorded) was rejected, not deferred this time, on the recording-decisions skill's own argument: gating on 'did you write a decision' rewards writing a junk one to clear the gate, and a base of junk teaches readers to skim. Keeping validate as convention was rejected because a broken pointer silently corrupts every later trace - the cheapest possible enforcement prevents the most expensive class of rot.

## Impact

Pushes fail on KB pointer breakage until fixed (one-time setup per clone: git config core.hooksPath .githooks). Capture quality remains a judgment reviewed by humans, per the no-junk-records principle. This narrows, not supersedes, the convention-first wiring decision: capture stance unchanged, integrity carved out.

Relates to [decision.adr-discipline-convention-first](decision.adr-discipline-convention-first.md).
