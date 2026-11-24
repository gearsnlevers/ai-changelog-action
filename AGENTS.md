# ai-changelog-action: instructions for coding agents

Updates the `## Unreleased` section of `CHANGELOG.md` with an LLM, preserves hand-written notes and can promote it to a release, and nothing else. It is a composite GitHub Action that release workflows use at its moving major tag (`gearsnlevers/ai-changelog-action@v1`). It is one of five small actions that release each other: version-bump-action, release-preflight-action, manifest-version-update-action, ai-changelog-action and npm-trusted-publish-action; each does one job and points to the others for the rest. Read [README.md](README.md) and `.github/agentic-workflows/scope.md` (what is in and out of scope) first.

## Layout

- `action.yml`: the interface (inputs, outputs, steps). `scripts/generate.js`: the implementation, which needs Node 20 and the production dependencies in `package.json` (`npm ci --omit=dev`). `test/generate.test.js`: its tests.
- `README.md`: the documented inputs and outputs, an example and the prerequisites.
- `.github/workflows/`: `ci.yml` and `release.yml` are this repository's own, and the `records-*.yml` workflows belong to Record Keeper (see Decisions). The rest belongs to the Repo Concierge (below).
- `CHANGELOG.md` is written by the Release workflow.

## Checks

- `npm test` runs `node --test` (`test/generate.test.js`). CI runs it.
- `node .github/record-keeper/record-keeper.mjs validate` checks the decision records.

## Rules

- **Inputs and outputs are a public interface.** Callers pin the major tag. Do not remove or rename an input or output, or change a default, in a way that changes what an existing caller gets. Add new ones with defaults that keep today's behaviour, and keep `action.yml` and the README in step.
- **Add or change a test in `test/` for every behaviour change.** The tests run the real script.
- **Stay within the action's job.** What is out of scope is listed in `.github/agentic-workflows/scope.md` with the sibling action to use instead; a change beyond it is a decision for a maintainer.
- **Do not edit `CHANGELOG.md` or the version in `package.json`.** The Release workflow writes both. A maintainer starts it by hand and reads every change to `.github/workflows/release.yml`.
- **Do not edit the Repo Concierge's files**: `.github/workflows/*.lock.yml` and the `.md` workflow sources beside them, `check-deployment.yml`, `concierge-updater.yml`, `dependency-watch.yml`, `janitor.yml`, `plan-approval-resume.yml`, `pr-ready-signal.yml`, `reporter-notify.yml`, the scripts of the same names (`check-deployment.mjs`, `concierge-updater.mjs`, `dependency-watch.mjs`, `janitor.mjs`, `plan-approval-resume.mjs`, `pr-ready-signal.mjs`, `reporter-notify.mjs`) in `.github/scripts/`, `.github/aw/`, `.gitattributes` and the pin in `.github/concierge.yml`. An update overwrites them. `.github/agentic-workflows/scope.md` belongs to this repository.
- **Never commit credentials.** This repository is public.

## Decisions

Accepted records are binding for humans and agents until a newer record supersedes them. If your task conflicts with one, stop and say so in the issue or pull request. A pull request that changes a decided behaviour adds or supersedes a record. Decisions for this repository are in [docs/decisions/](docs/decisions/README.md): To write one, use the [record-a-decision](.claude/skills/record-a-decision/SKILL.md) skill.

- [0001](docs/decisions/0001-the-action-writes-the-changelog-and-nothing-else.md): The action writes the changelog and nothing else.
- [0002](docs/decisions/0002-hand-written-unreleased-notes-survive.md): Hand-written Unreleased notes survive.
- [0003](docs/decisions/0003-the-model-s-output-is-checked-not-trusted.md): The model's output is checked, not trusted.
- [0004](docs/decisions/0004-a-full-release-consolidates-the-pre-release-notes.md): A full release consolidates the pre-release notes.
- [0005](docs/decisions/0005-the-llm-provider-is-the-caller-s-choice-and-the-key-is-required.md): The LLM provider is the caller's choice and the key is required.
- [0006](docs/decisions/0006-the-action-installs-its-own-production-dependencies-at-run-time.md): The action installs its own production dependencies at run time.
- [0007](docs/decisions/0007-releases-run-through-one-dispatched-workflow-that-uses-the-sibling-actions.md): Releases run through one dispatched workflow that uses the sibling actions.

<!-- record-keeper:begin -->
<!-- Managed by Record Keeper: the updater rewrites everything between the two markers, so a change made here is lost. Change the text in the kit. -->
## Decision records

Lasting decisions are kept as records in the folder named by `folder` in `.github/record-keeper/settings.yml` (`docs/decisions` when the setting is absent). Read its `README.md` and its index before you change behaviour that a record may cover.

- An accepted record binds people and coding agents. Never edit one. It changes only by a new record that supersedes it, by an erratum, or by an entry in its deviations section, and the owners approve all three.
- If your task conflicts with an accepted record, stop and say so in the issue or pull request. Do not work around the record.
- A pull request that changes a decided behaviour adds a record, or supersedes the old one, in the same pull request.
- To propose a decision, follow the `record-a-decision` skill in `.claude/skills/record-a-decision/SKILL.md`. Write the record with the status `proposed`.
- Never accept or seal a record. Accepting is an act of the owners, made in their own pull request.
- Numbers of records are never reused, and a record is never deleted, renamed or renumbered.
- Before you push a change to a record, run `node .github/record-keeper/record-keeper.mjs validate` (give the folder when it is not `docs/decisions`).
- Keep secrets, credentials, tenant names and personal data out of a record: it, its history and its pull request are read by many people.
<!-- record-keeper:end -->
