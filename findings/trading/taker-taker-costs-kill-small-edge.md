---
date: 2026-08-20
source_project: hyperliquid-bot
status: finding
confidence: high
---

# Taker-taker costs can kill small venue-spread edges

## Finding

Hyperliquid/Binanceの相対乖離やlead/lagを使った短期エッジは、costlessでは良く見えても、taker-taker前提だとほぼ死ぬことがある。

特に5秒〜60秒程度の短期signalで、平均利益が1〜3bps程度しかない場合、往復fee + spread + slippageで簡単にマイナスになる。

## Observed Pattern

HL/Binance basis mean reversionは、costlessだと一部銘柄で平均回帰がきれいに見えた。

しかしroundtrip costを入れると悪化した。

```text
0 bps cost: 一部プラス
1-2 bps cost: 銘柄/閾値次第
4 bps cost: かなり厳しい
10 bps cost: ほぼ不可
```

## Better Rule

短期裁定っぽい仮説は、まずtaker-takerで期待値を見る。そこで死ぬなら、次を検討する。

- makerで片足または両足を入れる
- 閾値を上げる
- horizonを伸ばす
- 板厚/約定確率を入れる
- signalを「basis逆張り」ではなく「lead-follow順張り」に変える

## Avoid

- costless backtestだけでBot化判断する
- 平均1bps台のedgeをtaker前提で信じる
- 勝率だけを見る

## Reuse

- Hyperliquid短期bot
- cross-venue arbitrage
- basis mean reversion
- lead/lag strategy
