---
date: 2026-08-20
source_project: codex-cross-thread/trading-backtests
status: rule
confidence: high
---

# Backtest Anti-Overfit Rule

## Rule

Never call a trading strategy robust because it wins inside the same data window used to discover it.

A backtest is only useful after comparing it with simple baselines, realistic costs, and at least one unseen period.

## Required checks

- Compare against a no-trade baseline.
- Compare against cash or short-term T-bill exposure when the objective is low drawdown.
- Include fees, spread, slippage, funding, borrow, and tax assumptions when relevant.
- Split research into train, validation, and unseen test periods.
- Report trade count. A strategy with very few trades is sample-dependent until proven otherwise.
- Treat a zero-trade result as a warning, not as a robust low-drawdown strategy.
- Avoid same-close execution unless the signal is available before that close.
- Check whether open positions at the end of the test are handled correctly.
- State the data source and known limitations, such as Yahoo data not matching exchange-specific execution.

## Common traps

- Drawdown minimization often selects no trade or cash-equivalent assets.
- Parameter sweeps can discover noise unless validated out of sample.
- Short-side rules often look attractive in narrative form but fail after rebounds, borrow/funding, and execution costs.
- Small edges that require taker-taker execution are usually destroyed by fees and spread.

## Reporting standard

When summarizing a strategy, include return, max drawdown, volatility, Sharpe-like ratio if useful, number of trades, average holding period, worst trade, best trade, and performance in unseen data.
