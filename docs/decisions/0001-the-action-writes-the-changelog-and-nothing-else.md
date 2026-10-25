---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - action.yml
  - scripts/generate.js
  - README.md
---

# The action writes the changelog and nothing else

## Context and problem statement

Release notes are one job, separate from versions, tags and publishing. Recorded retroactively from the README and `.github/agentic-workflows/scope.md`.

## Decision

- The action updates the `## Unreleased` section of the changelog from git history, diff statistics, merged pull requests and issues, and optionally related repositories, and can promote it to a versioned section and write the release notes to a file.
- It does not create tags or releases, publish, or edit any file other than the changelog. Those are other actions: version-bump-action (computes the version), release-preflight-action (checks collisions and drift), manifest-version-update-action (writes the version), ai-changelog-action (writes the changelog) and npm-trusted-publish-action (publishes).
- Other changelog formats or targets, additional LLM providers and model-specific behaviour need a maintainer's decision.

## Consequences

- Nothing else to watch; the decision is the boundary of the action.
