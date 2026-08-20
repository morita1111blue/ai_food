---
date: 2026-08-20
source_project: codex-cross-thread/cloudflare-os
status: rule
confidence: medium
---

# Cloudflare OS Safety Notes

## Rule

Local UI does not guarantee local-only data handling.

When using Cloudflare OS or similar local control panels, distinguish between where the interface runs, where credentials are stored, where model inference happens, and whether logs capture prompts or responses.

## Data exposure model

- A localhost UI is not public internet exposure by itself.
- Content retrieved from Gmail, Calendar, Drive, Notion, or other tools may still be sent to the model provider for inference.
- OAuth/API tokens should not be exposed to the model, but local files or environment variables may store tokens in readable form.
- AI Gateway payload logging can store prompts and responses if enabled.
- Tunnel/share features can expose a local service externally. Use them only intentionally.

## Safety checklist

- Rotate tokens after command-line testing or accidental exposure.
- Remove broad permissions that are not needed, especially BigQuery-like data access.
- Disable AI Gateway payload logs unless there is a specific reason to keep them.
- Do not send passwords, government IDs, private keys, seed phrases, or highly sensitive documents through model prompts.
- Check whether a service is truly local-only before assuming privacy.

## Model compatibility trap

If ordinary chat works but tool calls fail with HTTP 400, first suspect model/provider tool-call schema compatibility rather than auth or intelligence.

GPT-style open models may handle text chat while failing internal agent/tool calls. Test one simple tool call before investing time in prompt or permission debugging.

## Billing notes

Budget alerts are notifications, not hard caps. Workers Paid and Workers AI usage can create ongoing cost even when the UI feels local.
