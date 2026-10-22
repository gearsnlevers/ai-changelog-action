# Project scope

Read by the issue gate's scope check (Repo Concierge). The check is off for a repository without this file.

## Purpose

A reusable GitHub Action that updates the `## Unreleased` section of a repository's `CHANGELOG.md` using an LLM. It gathers git history and diff stats, merged pull requests, issues and optional related-repository activity, preserves existing Unreleased notes verbatim, and consolidates pre-release entries when preparing a stable release.

## In scope

- Generating and merging user-focused changelog entries into the Unreleased section
- Gathering the source material: git history, pull requests, issues, related repositories
- Preserving hand-written notes and consolidating pre-release notes for a stable release
- The action's inputs and outputs, documentation, tests, and release pipeline

## Out of scope

<!-- Every item here can close an issue automatically as not planned. Keep the list short and specific. -->

- Creating git tags, GitHub releases or publishing packages. The action only writes the changelog.
- Editing files other than the changelog, such as source code or the README.

## Needs a maintainer

- Other changelog formats or output targets, such as a GitHub Release body
- Additional LLM providers or model-specific behavior

## Where to go instead

- Versions, tags and publishing: version-bump-action, release-preflight-action, manifest-version-update-action and npm-trusted-publish-action.
