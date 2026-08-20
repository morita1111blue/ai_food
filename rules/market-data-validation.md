---
date: 2026-08-20
status: rule
confidence: medium
---

# Validate market data semantics before calculating spread

## Rule

価格差を計算する前に、必ずそれぞれの商品が何を参照しているかを確認する。

## Applies When

- 同じ企業・指数・商品を参照しているように見える複数銘柄を比較する
- ADR / ADS / ordinary share / FX conversion が絡む
- 複数venueのperp価格を比較する
- oracleやindex priceが利用できる

## Do

- contract annotation / exchangeInfo / metadata を読む
- oracle price と mid/mark price を分ける
- 名目価格差と正規化価格差を分ける
- 可能なら `(mid / oracle)` 同士を比較する
- 最後にfee、spread、depth、fundingを見る

## Avoid

- ticker名が似ているだけで同一商品とみなす
- `*10` のような名目換算だけを売買シグナルにする
- oracle差やFX差を見ずに乖離と判断する

## Evidence

`xyz:SKHX` / `xyz:SKHY` では、名目 `SKHY * 10` 比較だと約-25%に見えたが、oracle-normalizedでは約-1%前後だった。
