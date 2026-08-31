---
type: constraint
title: >-
  Dev install requires --legacy-peer-deps: react 19 tree vs
  @testing-library/react 14 peer range
description: >-
  The flag is install-time only, so nothing in the repo reveals it after the
  fact; without this record the next clean-machine setup rediscovers the failure
  the hard way.
tags:
  - setup
  - dependency-resurrection
generated:
  by: assafk
  at: '2026-08-31T05:53:23.174Z'
verified: []
strauss_anchors:
  - file: package.json
strauss_status: accepted
strauss_confidence: high
strauss_owner: assafk
---
## Claim

npm install on a fresh clone fails with an ERESOLVE conflict (react@19.2.8 in the tree, @testing-library/react@14 declaring peer react@^18) and must run with --legacy-peer-deps until the testing-library dependency is upgraded to a react-19-compatible major. package.json's devEngines block was also migrated from the legacy shorthand to the object form modern npm requires.

## Evidence

Verified on node 26, 2026-08-31: plain install fails ERESOLVE; flagged install plus the postinstall dll build and the full production build (main + renderer) all pass. Upstream Pile is dormant since Dec 2024; its tree predates react 19 peer-range updates.

## Implication

Every setup instruction and CI config must carry the flag. Exit paths: upgrade @testing-library/react to >=16, or pin react back to 18 - prefer the upgrade.
