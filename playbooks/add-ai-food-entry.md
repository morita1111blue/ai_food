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
