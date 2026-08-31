# CLAUDE.md

Pile: a local journaling desktop app (Electron + React, webpack/erb build).
Entries are markdown files on disk per pile; index, tags, links, and search are
derived local structures. No server, no accounts, no sync (yet — sync is the
next feature and its design decisions are pending).

## Setup

`npm install --legacy-peer-deps` (plain install fails ERESOLVE; see
`constraint.install-needs-legacy-peer-deps` in the KB). `npm run build`
verifies main + renderer.

## Knowledge base — the decision discipline

This repo carries a strauss-kb bundle at `.strauss/kb` (the CLI default; the
`kb_*` MCP tools take `bundlePath` to it). Set `STRAUSS_KB_ACTOR` to your name.
Decision records enter the workflow at three points:

1. **Before design — load.** Start any design or architecture work by loading
   the whole bundle (`strauss-kb load`); records arrive with standing, and
   superseded ones arrive as stubs. Design conversations build on records, and
   mid-session choices land as decision records at the moment the trade-off is
   live, not written up afterwards.
2. **At implementation boundaries — write.** Finishing a subtask requires
   either a decision record (`kb_write_decision`) or an explicit
   `kb_no_decision` — never silence. ALWAYS load the `recording-decisions`
   skill before writing one: it owns selectivity (record only what a later
   reader could not reconstruct from the diff; the rejected alternative earns
   the record) and what to attach — every decision anchors the files it
   shapes (`anchors`), cites what was read (`sources`), and links the records
   it rests on (`relatedConceptIds`).
3. **During review — read.** Judge changes against recorded decisions instead
   of re-litigating them. Review pushback that genuinely changes a decision
   supersedes the record in the same cycle (`kb_supersede`) — never edit or
   delete a record whose meaning changed.

KB integrity is enforced at push: a pre-push hook runs `strauss-kb validate`
and blocks on anything but `[]` (one-time setup:
`git config core.hooksPath .githooks`).

Capture itself is still convention, not enforcement: nothing mechanically
blocks a turn on a missing decision record (recorded honestly — the why-gate
is deferred until capture measurably drops).
