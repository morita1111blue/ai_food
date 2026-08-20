---
date: 2026-08-20
source_project: hyperliquid-bot
status: intake
confidence: medium
promote_to_rule: true
---

# SKHX / SKHY dual listing spread

## Context

Hyperliquid `xyz` 上に、SK hynix を参照するように見える銘柄が2つあった。

- `xyz:SKHX`
- `xyz:SKHY`

この価格差を監視するWebページを作った。

## Observation

Hyperliquid annotation上の意味は次の通り。

- `xyz:SKHX`: KRXのSK hynix普通株1株をUSD換算したもの
- `xyz:SKHY`: Nasdaq ADSのSKHY。普通株の1/10を表す

ただし、売買判断用のspreadを `SKHX / (SKHY * 10) - 1` で見るのは雑だった。

## Mistake / Trap

名目上は `SKHY * 10` が普通株換算に見えるが、実際にはFX、オラクル参照、ADS、取引時間、流動性差が混ざる。

そのため、名目差は大きく見えすぎる。今回も名目では約-25%の差が出たが、オラクル正規化後は約-1%前後だった。

## Better Rule Candidate

dual listing / ADS / FX-linked perpのspreadは、まず各銘柄のoracleを確認する。

メイン指標は原則として、名目価格差ではなく相対プレミアム差にする。

```text
(SKHX mid / SKHX oracle) / (SKHY mid / SKHY oracle) - 1
```

## Reuse

- Hyperliquid `xyz` の株式perp
- ADR / ADS 系の銘柄
- FX換算された株式perp
- 同一企業を複数venueまたは複数証券形態で参照する商品

## Evidence

Hyperliquid Info API:

```text
POST https://api.hyperliquid.xyz/info
{"type":"metaAndAssetCtxs","dex":"xyz"}
```

Annotation API:

```text
{"type":"perpAnnotation","coin":"xyz:SKHX"}
{"type":"perpAnnotation","coin":"xyz:SKHY"}
```

実装先:

```text
hyperliquid-bot/dashboard/skhynix-spread/
hyperliquid-bot/dashboard/server.py
```
