---
date: 2026-08-20
source_project: hyperliquid-bot
status: intake
confidence: high
promote_to_rule: false
---

# TradFi perp collector design notes

## Context

Hyperliquid上のTradFi系perpを24時間収集し、翌日に短期売買の市場構造を分析する仕組みを作った。

初期目的は次の検証だった。

- OI washout後のリバウンド
- aggressive buy/sell exhaustion
- 板の流動性回復
- Binance ↔ Hyperliquid lead/lag
- venue間価格乖離
- OI / order flowによるtrend continuation

## Observation

対象銘柄はハードコードしない。Hyperliquid `xyz` 上のTradFiっぽい銘柄を出来高上位から自動選択し、同じ原資産がBinanceにもある場合だけBinance側も収集するのが実用的だった。

HyperliquidのTradFi系銘柄は次で取る。

```text
POST https://api.hyperliquid.xyz/info
{"type":"metaAndAssetCtxs","dex":"xyz"}
```

収集粒度は初版では次が現実的。

```text
trades: 全件WebSocket
book: 5秒
mark/oracle/mid: 5秒
open interest: 5秒
funding: ctx取得時
```

保存はParquet + DuckDBが扱いやすい。途中停止しても失わないように1時間程度でrotateする。

## Mistake / Trap

Binance側のTradFi perpetualは通常のcrypto perpetualだけではなく、`TRADIFI_PERPETUAL` のようなcontract typeが出ることがある。

`PERPETUAL` だけでfilterすると、Binanceに存在するはずのSNDK/GOOGLBなどを見落とす可能性がある。

## Better Rule Candidate

Hyperliquidで触れるTradFi銘柄を主軸にし、Binanceは比較用venueとして後からattachする。

```text
HL xyz top volume
-> canonical_underlyingを作る
-> Binance exchangeInfoで同一/近似symbolを探す
-> 両方取れるものだけlead/lagやbasisを分析
```

## Reuse

- Hyperliquid `xyz` の新規TradFi銘柄収集
- 翌日レポート生成
- venue間lead/lag検証
- 自動売買前のデータ品質チェック
