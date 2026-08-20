---
date: 2026-08-20
source_project: hyperliquid-bot
status: finding
confidence: medium
---

# Binance shock to Hyperliquid lead-follow was more promising than basis reversal

## Finding

2日分のTradFi perp収集データでは、HL/Binance basis mean reversionより、Binanceの急変を見てHyperliquid側で同方向に乗るlead-followの方が有望に見えた。

## Observed Pattern

Binance 5秒moveをsignalにして、HLで同方向に入るbacktestでは、一部銘柄が手数料1〜2bpsでも比較的残った。

特にSPCX/SKHY/SNDK/MUなどに候補があった。

ただし、これはまだデータ日数が少ない。

## Better Rule Candidate

cross-venue分析では、まず次の順で見る。

1. 同一/近似原資産のデータ品質
2. 5秒/10秒/30秒/60秒のlead-lag相関
3. costlessの方向性
4. taker cost 1/2/4bps後の残り方
5. 日別のmin performance
6. liquidity / fillability

## Avoid

- basis乖離が見えた瞬間に逆張りBot化する
- 1日だけの結果で判断する
- fee2bpsで残らないものをtaker strategyにする

## Reuse

- TradFi perp lead/lag検証
- Binance reference / HL executionの仮説
- signal candidate filtering
