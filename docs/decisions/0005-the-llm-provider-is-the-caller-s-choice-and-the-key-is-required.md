---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - action.yml
  - scripts/generate.js
seal: sha256-g1:5a432fe77f64ba71db62fdea6574028480e16f1c280555869a86c199b3af0b88
---

# The LLM provider is the caller's choice and the key is required

## Context and problem statement

Callers have different providers and budgets. Recorded retroactively from the inputs and the README.

## Decision

- `llm-provider` is `openai` (the default) or `anthropic`, and `model` names the model for that provider.
- `llm-api-key` is required: the action fails without it and never has a built-in key. Other providers need a maintainer's decision.

## Consequences

- Both provider SDKs are production dependencies.
