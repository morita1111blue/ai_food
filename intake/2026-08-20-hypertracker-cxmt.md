---
date: 2026-08-20
source_project: hyperliquid-bot
status: intake
confidence: medium
promote_to_rule: false
---

# HyperTracker CXMT position and liquidation data

## Context

Hyperliquid公式APIだけでは、特定銘柄で大きなポジションを持つ上位アカウント一覧を直接取得しづらい。

`xyz:CXMT` について、HyperTracker / CoinMarketMan のページを調べた。

## Observation

HyperTrackerのSPA裏に、銘柄別の公開JSONがあった。

Base:

```text
https://dw3ji7n7thadj.cloudfront.net/aggregator
```

例:

```text
/assets/active.json
/assets/xyz:CXMT/positions.json
/assets/xyz:CXMT/liquidation-heatmap.json
/assets/xyz:CXMT/position-metrics_v2.json
/assets/xyz:CXMT/coin-position-breakdown-by-size.json
/assets/xyz:CXMT/coin-position-breakdown-by-cohort.json
```

## Useful Data

- 上位ポジション
- side
- address
- position value
- entry price
- liquidation price
- unrealized PnL
- liquidation progress
- size cohort
- liquidation heatmap

## Mistake / Trap

公式APIで全アカウントを総当たりする発想は現実的ではない。

既知アドレスの `clearinghouseState` は取れるが、銘柄別の大口ランキングは公式だけでは見つけづらい。

## Better Rule Candidate

Hyperliquidで「大口」「清算帯」「口座別偏り」を見る時は、まず公式APIで取れる範囲と、HyperTrackerの集計済み公開JSONを分けて考える。

公式API:

- 正確な個別アカウント状態
- 既知アドレスの検証

HyperTracker:

- 銘柄別上位ポジション
- 清算ヒートマップ
- size cohort

## Reuse

- CXMT以外の `xyz:*` 銘柄
- 清算帯接近アラート
- 大口ポジション監視
- OI washout / liquidation cascade 仮説の検証
