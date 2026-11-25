---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - scripts/generate.js
seal: sha256-g1:7c20f7ce5d328cab996a3fba71470a4812d3c718e1ca37bfd555f47da92a1b9c
---

# The model's output is checked, not trusted

## Context and problem statement

The model alone produced duplicate bullets and bullets under the wrong heading (commit 802dbab). Recorded retroactively from the script and commits 63e70ad (the grounding filter and the commit-based notes) and 802dbab.

## Decision

- A generated bullet is kept only if it cites a commit or pull request that is in the evidence gathered for this release. If nothing survives, notes built from the commit subjects are used.
- Headings are normalized to the Keep a Changelog categories and bullets are deduplicated across sections by a deterministic pass. Lines that repeat the previous release's notes are removed, unless pre-release notes are being consolidated.
- When the release changes only files under `.github/`, or no functional file, and there are no hand-written or pre-release notes, a fixed sentence is used and the model is not called.

## Consequences

- A change with no commit or pull request behind it cannot appear in the notes.
