---
date: 2026-08-20
status: rule
confidence: medium
---

# Dashboard UI should optimize for scan density, not decorative layout

## Rule

運用・市場監視系のdashboardは、装飾よりも一覧性とスキャン性を優先する。

## Applies When

- Market Health
- Surge ranking
- Turnover ranking
- Pair/spread monitor
- Ops/status pages

## Do

- 主要項目を一画面に収める
- 表の列幅を詰める
- 横スクロールを減らす
- チャートの軸ラベルを十分に出す
- 現在値は残しつつ履歴グラフも出す
- 名前やラベルが切れないようにする
- 重要な変化は同じセル内で視認できるようにする

## Avoid

- カードを増やしすぎて一画面で見えなくする
- 名前が切れる凡例
- 横軸ラベルが左右端だけのチャート
- 変化なしを `→0` などで目立たせる
- 表示のためだけの冗長な列

## Evidence

ユーザーはMarket Healthで「主要項目を全部一画面で見たい」、rankingで「極力横スクロールなし」、SK hynix spreadで「横軸の時間表示を増やしてほしい」と明示した。
