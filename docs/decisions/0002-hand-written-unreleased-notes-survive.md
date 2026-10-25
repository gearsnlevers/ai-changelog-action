---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - scripts/generate.js
  - README.md
---

# Hand-written Unreleased notes survive

## Context and problem statement

Maintainers write notes by hand during a cycle and expect them to be in the release. A generated entry must not replace or duplicate them. Recorded retroactively from the README, `mergePreservingExistingUnreleased` and commits b97b937, 29a5ed3 and 802dbab.

## Decision

- Existing entries under `## Unreleased` are kept. Generated lines are merged in as additions.
- A generated bullet that is a near-duplicate of an existing one is never appended as a second bullet. A thinner existing bullet is expanded in place with the fuller generated wording; a bullet that is already as detailed is left untouched.
- A verbose existing bullet, including one written by a coding agent, may be tightened only when the rewrite keeps every flag and every commit or pull request reference the original has. With no such marker to check, the original is kept.

## Consequences

- A hand-written note is never lost, but a thin one can grow.

## Known deviations

The README promises that existing notes are kept verbatim. Since v1.1.12 a thin note can be expanded and a verbose one tightened as described above, so the README states the guarantee more strongly than the code.
