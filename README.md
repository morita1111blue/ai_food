# ai_food

AIが仕事をしながら獲得した知見を、次のAIが使える判断材料として残すためのリポジトリです。

ここに置くものは、単なる作業ログではありません。次回以降のAIの判断・調査順序・実装方針を変える可能性がある知見だけを残します。

## AI向け入口

このリポジトリを育てるAIは、作業前に必ず次の2ファイルを読んでください。

- `AI_INSTRUCTIONS.md`: AIがこのrepoを扱うときの実務指示。
- `CONTRIBUTING.md`: 追加・更新・重複防止・秘密情報回避のルール。

## 目的

新しいチャットや別案件で、昨日到達した地点を今日のスタート地点にする。

```text
work
-> observe
-> record reusable knowledge
-> see the same structure again
-> promote to rule/playbook
-> next AI starts ahead
```

## ディレクトリ

```text
intake/      その日の作業から得た知見。まずここに入れる。
findings/    再利用できる発見として整理したもの。
rules/       複数回確認され、次回AIが最初から従うべき判断ルール。
playbooks/   手順化できる作業。チェックリストとして使う。
templates/   新しい知見を書くための型。
```

## 残す基準

残すもの:

- 同じ失敗をもう一度防げるもの
- 次回の調査手順を短縮できるもの
- API、データ取得元、仕様、制約の発見
- 実装判断の根拠
- 期待と違った結果
- 売買仮説が死んだ理由

残さないもの:

- その場限りの雑談
- 長すぎる生ログ
- コードを読めば明らかなこと
- 未検証の思いつきだけ
- 同じ内容の重複

## 昇格ルール

```text
intake: まず記録する
findings: 別の仕事でも使えそうなら整理する
rules: 同じ構造が複数回確認されたら判断ルールにする
playbooks: 手順として再実行できるならチェックリスト化する
```

## 書き方

各ファイルには、できるだけ次を入れます。

```yaml
---
date: YYYY-MM-DD
source_project: project-name
status: intake | finding | rule | playbook
confidence: low | medium | high
promote_to_rule: false
---
```

重要なのは、きれいな文章よりも「次のAIの判断が変わること」です。
