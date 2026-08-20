---
date: 2026-08-20
status: playbook
confidence: high
---

# Commit and push safely with a mixed worktree

## Scope

作業repoにユーザー由来または過去作業由来の未コミット変更が混ざっている時に、自分の変更だけcommit/pushする。

## Rule

`git add -A` を使わない。必ず対象ファイルを明示してstageする。

## Steps

1. 状態確認

```bash
git status --short
```

2. 対象差分だけ確認

```bash
git diff -- path/to/file1 path/to/file2
```

3. 対象ファイルだけstage

```bash
git add path/to/file1 path/to/file2
```

4. staged diff確認

```bash
git diff --cached --stat
git diff --cached
```

5. commit

```bash
git commit -m "Short message"
```

6. GitHub token headerでpushできる場合

```bash
TOKEN=$(gh auth token)
AUTH=$(printf 'x-access-token:%s' "$TOKEN" | base64 -w0)
GIT_TERMINAL_PROMPT=0 git -c "http.extraHeader=Authorization: Basic ${AUTH}" push --progress origin main
```

## Avoid

- unrelatedな `RESEARCH_LOG.md` などを巻き込む
- 未追跡ディレクトリを確認なしでstageする
- `git reset --hard` や `git checkout --` でユーザー変更を消す

## Reuse

- hyperliquid-bot
- ai_food
- 複数repoをまたぐ作業
