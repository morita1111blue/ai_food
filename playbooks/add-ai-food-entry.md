---
date: 2026-08-20
status: playbook
confidence: high
---

# Add an entry to ai_food

## Steps

1. 今回の作業から、未来のAIの判断を変えるものを1〜3個だけ選ぶ。
2. まず `intake/YYYY-MM-DD-topic.md` に書く。
3. すでに再利用性が明確なら `findings/<domain>/` にも整理する。
4. 複数回確認済みなら `rules/` に入れる。
5. 手順なら `playbooks/` に入れる。
6. 秘密情報を検索する。
7. commit/pushする。

## Deduplication

Before creating a new entry, read the existing Markdown files under `intake`, `findings`, `rules`, and `playbooks`.

- If the same or very similar knowledge already exists, do not create a new file.
- If the new observation strengthens or clarifies an existing entry, update that file instead.
- If the existing entry conflicts with the new observation, stop and ask the user before editing.
- Prefer one durable rule or playbook over many near-duplicate intake notes.
- For automated maintenance, only self-commit high-confidence, non-sensitive, non-duplicate updates that fit the existing structure. Ask first when uncertain.

## Minimal Secret Check

```bash
grep -RInE "webhook|token|gho_|api[_-]?key|secret|password" . --exclude-dir=.git || true
```

## Commit

```bash
git status -sb
git add <explicit files>
git diff --cached --stat
git commit -m "Add knowledge entries"
git push
```

## Good Entry Shape

```md
---
date: YYYY-MM-DD
source_project: project
status: intake
confidence: medium
promote_to_rule: false
---

# Title

## Context
## Observation
## Mistake / Trap
## Better Rule Candidate
## Reuse
## Evidence
```
