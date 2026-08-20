---
date: 2026-08-20
status: rule
confidence: medium
---

# Promote repeated observations into reusable AI rules

## Rule

`ai_food` は単なるログ置き場ではなく、未来のAIの判断を変える外部知能として使う。

## Do

- 作業後に、再利用可能な知見があるか確認する
- まず `intake/` に短く残す
- 別案件でも使えそうなら `findings/` に整理する
- 同じ構造を複数回見たら `rules/` に昇格する
- 手順として再実行できるなら `playbooks/` にする

## Promote When

- 同じ失敗を防げる
- 次回の調査順序が変わる
- 実装判断が変わる
- 売買仮説の採否が変わる
- デプロイやGit操作の安全性が上がる

## Avoid

- 生ログを大量に置く
- 未検証の思いつきをruleにする
- 1回だけの観察を強いルールにする
- READMEや宣伝文のような判断に使わない文章を増やす

## Reuse

すべてのプロジェクト。特に新しいチャットや別repo作業の開始時。
