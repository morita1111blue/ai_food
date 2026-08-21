---
date: 2026-08-21
source_project: codex/ai-food-ops
status: playbook
confidence: high
---

# Prompt board for reusable AI instructions

## Purpose

Frequently reused AI instructions should not live only inside chat history.

If the user needs to reuse a prompt across Codex, ChatGPT Classic, Sites, or other AI services, create a stable prompt board with copy buttons instead of relying on scrolling, pinned chats, or memory.

## When To Use

Use this pattern when:

- the user repeatedly needs the same prompt in another AI service
- the prompt is operational rather than project-specific source code
- the user asks for something to be always visible or immediately reusable
- chat history search would be too slow or annoying

## Better Pattern

Create a small HTML prompt board with:

- one section per reusable prompt
- visible title for each prompt
- a copy button per block
- preformatted text that can be copied without editing
- no secrets embedded in the prompt

If the user already has a persistent dashboard, expose it as a standalone page there. A local HTML file is fine for personal use, but a dashboard page is better when it should be available from the same browser/workflow across machines.

## Avoid

- saying "it is in the chat above" when the user needs frequent reuse
- relying only on pinned chats for operational snippets
- mixing secrets or live credentials into reusable prompts
- creating many one-off prompt files when one board with sections is enough

## Reuse

- ai_food contribution prompts
- Sites plugin starter prompts
- cross-AI handoff prompts
- common GitHub PR or review prompts
