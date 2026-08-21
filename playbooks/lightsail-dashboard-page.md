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


## Narrow Static-Only Deploy

If a full deploy script has broad side effects such as `rsync --delete`, dependency installation, systemd unit installation, timer changes, or background collector starts, do not use it for a static page-only change.

For a static page and top-page link, transfer only the changed files, then restart only the dashboard process. If shell quoting becomes fragile, write a short remote deploy script and upload that script instead of building a long nested SSH command.

```bash
tar -czf /tmp/page-update.tar.gz dashboard/index.html dashboard/new-page/index.html
scp /tmp/page-update.tar.gz hyperliquid-lightsail:/tmp/page-update.tar.gz
scp /tmp/remote-deploy.sh hyperliquid-lightsail:/tmp/remote-deploy.sh
ssh hyperliquid-lightsail 'bash /tmp/remote-deploy.sh; rm -f /tmp/remote-deploy.sh'
```

Verify the external URL after the restart:

```bash
curl -s -o /dev/null -w "%{http_code}\n" http://100.74.138.70:8080/status
curl -s -o /dev/null -w "%{http_code}\n" http://100.74.138.70:8080/new-page/
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
