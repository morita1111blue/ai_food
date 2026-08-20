---
date: 2026-08-20
source_project: hyperliquid-bot
status: finding
confidence: medium
---

# Dual listing spread should be oracle-normalized

## Finding

同じ企業を参照しているように見えるperp同士でも、名目価格を直接比較すると誤解しやすい。

特に次が絡む場合は危険。

- ADS / ADR
- 普通株との交換比率
- FX換算
- venue差
- oracle差
- 取引時間差

## Preferred Formula

各銘柄が自分のoracleに対してどれだけpremium/discountで取引されているかを比較する。

```text
normalized_spread = (A_mid / A_oracle) / (B_mid / B_oracle) - 1
```

## Why

名目価格差は、商品の定義やFX水準を反映しすぎる。

相対プレミアム差は、各商品のフェア値からのズレを比較するので、短期監視に向いている。

## Still Required

売買シグナル化する前に、次を見る。

- bid/ask spread
- 板厚
- funding差
- oracle更新タイミング
- 取引時間
- taker/maker cost
