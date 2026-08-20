---
date: 2026-08-20
source_project: hyperliquid-bot
status: intake
confidence: high
promote_to_rule: true
---

# Lightsail dashboard partial deploy

## Context

`hyperliquid-bot` のダッシュボードに新ページを追加し、Lightsailへ反映した。

フルの `deploy.sh` は `rsync --delete` を含み、サービス再起動や常駐ジョブ有効化も行うため、軽微なページ追加には副作用が広い。

## Observation

対象ファイルだけをrsyncし、`hyperliquid-dashboard.service` だけを再起動する方が安全だった。

## Safer Deploy Pattern

```bash
rsync -az dashboard/server.py dashboard/index.html hyperliquid-lightsail:/home/ubuntu/hyperliquid-bot/dashboard/
rsync -az dashboard/skhynix-spread/index.html hyperliquid-lightsail:/home/ubuntu/hyperliquid-bot/dashboard/skhynix-spread/
ssh hyperliquid-lightsail "sudo systemctl restart hyperliquid-dashboard.service"
```

Verify:

```bash
ssh hyperliquid-lightsail "systemctl is-active hyperliquid-dashboard.service"
ssh hyperliquid-lightsail "python3 - <<'PY'
import urllib.request
for path in ['/status', '/skhynix-spread/', '/api/skhynix-spread?hours=1']:
    with urllib.request.urlopen('http://127.0.0.1:8080' + path, timeout=10) as r:
        print(path, r.status, r.headers.get('Content-Type'))
PY"
```

External check:

```text
http://100.74.138.70:8080/<path>
```

## Mistake / Trap

`systemctl is-active` が `active` でも、再起動直後はHTTP確認が一瞬 `Connection refused` になることがある。数秒待って再試行する。

## Rule Candidate

軽微な静的ページ/API追加では、まず部分デプロイを選ぶ。フルdeployは、依存関係・opsファイル・全体同期が必要な時だけ使う。
