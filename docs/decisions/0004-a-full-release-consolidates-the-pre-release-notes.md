---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - scripts/generate.js
  - README.md
---

# A full release consolidates the pre-release notes

## Context and problem statement

Notes are written during the alpha, beta or release-candidate cycle, and the stable release should read as one clean set. Recorded retroactively from the README.

## Decision

- For a full (stable) release the action finds every pre-release tag since the previous full release and collects the notes written for them, first from the sections already in the changelog and then from GitHub release bodies.
- It gives all of that to the model to produce de-duplicated, consolidated notes for the stable version. `release-type` is `auto`, `full` or `prerelease`; `auto` detects it.

## Consequences

- Pre-release notes written well are reused, written badly they carry over.
