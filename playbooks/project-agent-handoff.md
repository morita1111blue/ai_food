---
date: 2026-08-20
source_project: codex-cross-thread/codex-project-ops
status: playbook
confidence: high
---

# Project Agent Handoff

## Purpose

Give future Codex sessions enough context to start from the current project state instead of rediscovering the environment.

Use this as a checklist for `AGENTS.md`, `README.md`, or handoff notes in active repositories.

## Required sections

- Project purpose and current stage.
- Canonical local path and remote repository.
- Runtime environment, including Windows vs WSL expectations.
- Install, test, run, stop, and deploy commands.
- Production host, service names, ports, and log locations when applicable.
- Known dirty files or user-owned changes that should not be reverted.
- Secret locations and handling rules, without storing actual secrets.
- Safety boundaries, especially for trading, production writes, and paid APIs.
- Verification checklist before claiming completion.
- Documentation files that should be updated when behavior changes.

## Trading project additions

- State clearly whether live order placement is allowed.
- Separate data collection, backtesting, paper trading, and production trading stages.
- Require fee, spread, slippage, funding, and position limit assumptions in strategy tests.
- Require explicit user approval before enabling auto-ordering or changing risk limits.

## Deploy project additions

- Record the exact deploy command that worked.
- Record health-check URLs.
- Record common failure modes and recovery commands.
- Record whether deployment should happen automatically after push or only after explicit request.
