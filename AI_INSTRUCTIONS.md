# AI Instructions

You are helping maintain `ai_food`, a shared knowledge base for future AI agents.

Your goal is not to summarize everything. Your goal is to preserve only the knowledge that can change a future AI agent's judgment, investigation order, implementation approach, or risk handling.

## Required First Steps

1. Read `README.md`.
2. Read `CONTRIBUTING.md`.
3. Read the existing Markdown files most likely to overlap with the new knowledge.
4. Decide whether the new content is a new entry, an update to an existing entry, or not worth adding.

## Selection Standard

Keep knowledge if it helps a future agent:

- avoid a known trap
- validate market data or API semantics
- choose safer deployment, Git, or automation behavior
- understand user preferences that affect implementation
- reject a weak trading hypothesis for a reusable reason
- run a repeatable workflow with less rediscovery

Skip knowledge if it is:

- one-shot and unlikely to recur
- too specific to one temporary event
- already captured elsewhere
- speculative without evidence
- sensitive, private, or secret-bearing

## Deduplication

Before creating a file, search the repo. If similar knowledge exists, update that file instead. Prefer one durable rule or playbook over many near-duplicate notes.

If the best action is updating an existing file, say which file and why.

## Output Shape

When proposing additions to a human, use this format:

```text
Candidate:
Destination:
New file or update:
Why it matters:
Confidence:
Sensitive data risk:
```

When directly editing, include frontmatter when useful:

```yaml
---
date: YYYY-MM-DD
source_project: project-or-thread
status: intake | finding | rule | playbook
confidence: low | medium | high
---
```

## Safety

Never store actual secrets, tokens, webhook URLs, private keys, account numbers, or raw personal data.

When in doubt, ask the user before writing.
