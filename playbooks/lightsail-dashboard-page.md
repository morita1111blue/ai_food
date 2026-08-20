---
date: 2026-08-20
status: playbook
confidence: high
---

# Add a dashboard page to Lightsail safely

## Scope

`hyperliquid-bot` の既存dashboardに、新しいページ/APIを追加してLightsailへ反映する。

## Steps

1. ローカルでページ/APIを追加する。
2. `python3 -m py_compile dashboard/server.py` を実行する。
3. ローカルサーバーで対象ページ/APIを確認する。
4. 対象ファイルだけをrsyncする。
5. `hyperliquid-dashboard.service` だけ再起動する。
6. サーバー内HTTPで `/status` と対象APIを確認する。
7. Tailscale URLで外から確認する。
8. commit/pushする。

## Partial Deploy Example

```bash
rsync -az dashboard/server.py dashboard/index.html hyperliquid-lightsail:/home/ubuntu/hyperliquid-bot/dashboard/
rsync -az dashboard/new-page/index.html hyperliquid-lightsail:/home/ubuntu/hyperliquid-bot/dashboard/new-page/
ssh hyperliquid-lightsail "sudo systemctl restart hyperliquid-dashboard.service"
```

## Verify

```bash
ssh hyperliquid-lightsail "systemctl is-active hyperliquid-dashboard.service"
ssh hyperliquid-lightsail "python3 - <<'PY'
import urllib.request
for path in ['/status', '/new-page/', '/api/new-page']:
    with urllib.request.urlopen('http://127.0.0.1:8080' + path, timeout=10) as r:
        print(path, r.status)
PY"
```

## Avoid

フル `deploy.sh` は `rsync --delete` を含むため、ページ1枚の反映ではまず使わない。
