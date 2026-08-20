---
date: 2026-08-20
source_project: codex-cross-thread/x-obsidian
status: playbook
confidence: medium
---

# X Likes To Obsidian

## Purpose

Archive liked X posts into Obsidian without depending on fragile scraping or expensive always-on API access.

## Preferred path

Use the official X data archive as the primary source, then import liked posts into Markdown.

This is slower than real-time sync, but it is stable, low-cost, and avoids browser automation fragility.

## Note format

Create one Markdown file per liked post.

Recommended frontmatter:

```yaml
type: x-like
source: x
post_id:
author:
url:
posted_at:
fetched_at:
tags:
  - x-like
```

Keep the post ID as the durable dedupe key.

## Sync cadence

Monthly archive refresh is more realistic than free real-time sync.

Manual clipping can complement the archive flow for posts that are important immediately.

## Avoid by default

- Browser automation against the live X UI.
- Paid API reads unless the value of real-time sync is clear.
- Saving only screenshots without post ID or URL.
