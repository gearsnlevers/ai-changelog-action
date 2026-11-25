---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - action.yml
  - package.json
  - package-lock.json
seal: sha256-g1:dd051a6f0504b72886eda0d07574a0e6747fa6ff48d79cbab0e9a9591be0a235
---

# The action installs its own production dependencies at run time

## Context and problem statement

The action is a Node script that needs the GitHub and provider SDKs, and the repository does not commit `node_modules`. Recorded retroactively from `action.yml`.

## Decision

- The composite action sets up Node, runs `npm ci --omit=dev` in the action's own directory, then runs the script.
- `package-lock.json` is committed so every run installs the same versions.

## Consequences

- Each run pays for an install, and a dependency change is a change to the lock file.
