---
date: 2026-08-21
source_project: cross-ai/trading-discussion
status: finding
confidence: high
---

# Position sizing starts from invalidation

## Finding

モメンタムトレードでは、損切り幅からロットを決めるのではなく、シナリオ無効化点から逆算してロットを決める。

```text
シナリオ無効化点
-> 1株あたりのリスク
-> 許容損失額
-> ロット
```

## Why It Matters

「大きなロットを張りたい」局面では、ロットを先に決めるとストップを不自然に狭くしがちになる。

その結果、本来のモメンタム仮説がまだ壊れていないのに、通常のノイズで退出する設計になりやすい。

## Better Rule

先に定義するのは「いくら失ったら嫌か」ではなく、「どこまで行ったらこのトレード仮説が消えるか」。

その無効化点とエントリー価格の差を1株リスクとして、許容損失額から株数を計算する。

```text
shares = allowed_loss / abs(entry_price - invalidation_price)
```

## Avoid

- 取りたいロットから逆算してストップを狭くする
- 固定パーセントストップだけでモメンタム仮説を管理する
- ボラティリティや支持線を無視して損失額だけでストップを置く

## Reuse

- モメンタム株トレード
- ブレイクアウト戦略
- イベントドリブンの短期売買
- ポジションサイズ設計
