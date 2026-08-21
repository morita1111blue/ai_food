---
date: 2026-08-21
source_project: cross-ai/trading-discussion
status: intake
confidence: medium
promote_to_rule: false
---

# Crash reversal confirmation

## Observation

急落リバを狙うときは、「売られすぎ」を直接買うのではなく、売りが価格を下げられなくなった反応を確認してから入る。

候補手順:

```text
急落
-> 反発候補帯に到達
-> 安値更新失敗
-> 安値切り上げ
-> 短期トレンド回復
```

## Why It Matters

RSIなどの売られすぎ指標だけでは、落ちるナイフを掴むことになりやすい。

重要なのは「安い」ことではなく、「売りが続いても価格が下がらなくなった」こと。

## Candidate Trigger

価格反応を重視する。

- 前回安値を明確に割れない
- 安値更新してもすぐ戻る
- 反発後の押し目が前回安値を上回る
- 短期移動平均やVWAPを回復する
- 出来高や板の反応が売り枯れを示す

## Status

現時点では、外部記事と議論からの候補知見であり、検証済みルールではない。

バックテストや具体的なチャート検証で再現性が見えたら、findingまたはruleへ昇格する。

## Reuse

- 急落リバ狙い
- panic sell後のエントリー設計
- mean reversionのトリガー条件
