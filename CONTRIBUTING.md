# Contributing to ai_food

`ai_food` is not a general notes repo. It stores reusable knowledge that can change how a future AI agent investigates, decides, implements, or avoids mistakes.

## Before Adding

1. Read `README.md` and `AI_INSTRUCTIONS.md`.
2. Search existing Markdown files under `intake/`, `findings/`, `rules/`, and `playbooks/`.
3. If the same or very similar knowledge already exists, update the existing file instead of creating a new one.
4. If the new observation conflicts with existing knowledge, ask the user before changing it.
5. Do not add secrets, raw private logs, API keys, webhook URLs, account details, or sensitive personal information.

## What Belongs Here

Add knowledge when it helps a future AI agent do at least one of these:

- avoid repeating a mistake
- choose a better investigation order
- validate data or assumptions more carefully
- make a safer implementation or deployment decision
- reject a trading or automation hypothesis with a clear reason
- reuse a workflow as a playbook

## What Does Not Belong Here

Do not add:

- casual conversation
- one-shot trivia that will not affect future decisions
- raw transcripts or large logs
- unverified ideas promoted directly into rules
- duplicate files with different wording
- content that is obvious from source code alone

## Placement

- `intake/`: early observations worth preserving, not yet generalized
- `findings/`: reusable discoveries with some evidence
- `rules/`: repeated or high-confidence judgment rules future AI should follow
- `playbooks/`: repeatable procedures and checklists
- `templates/`: writing templates only

## Promotion

Prefer gradual promotion:

```text
intake -> finding -> rule/playbook
```

A single observation can be useful, but it should not become a strong rule unless it is high-confidence or has appeared across multiple tasks.

## Commit Standard

Before committing:

```bash
grep -RInE "webhook|token|gho_|api[_-]?key|secret|password|discord.com/api" . --exclude-dir=.git || true
git diff --check
git status -sb
```

Commit messages should describe the knowledge added, not the chat that produced it.
