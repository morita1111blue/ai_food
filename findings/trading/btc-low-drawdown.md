---
date: 2026-08-20
source_project: codex-cross-thread/trading-backtests
status: finding
confidence: medium
---

# BTC Low-Drawdown Strategy Finding

## Finding

For BTC, low-drawdown research favored daily trend exposure control over frequent short-term trading.

In prior experiments, one-hour strategies were vulnerable to noise and transaction costs. Daily trend-following rules with cash exits were more promising, especially when combined with hysteresis and volatility targeting.

## Practical implication

For a low-drawdown BTC strategy, start with long-or-cash exposure before adding short exposure.

Short rules can look attractive during selloffs, but they often enter late and suffer during sharp rebounds. Treat shorting as a separate high-risk strategy rather than a default part of a low-drawdown system.

## Candidate structure

- Daily signal frequency.
- SMA200 or similar long-term trend filter.
- Hysteresis band to reduce whipsaw, such as requiring price to move several percent beyond the threshold before switching.
- Volatility targeting to reduce exposure during high-volatility regimes.
- Cash or T-bill proxy when out of BTC.

## Validation requirements

- Include fees, spread, and slippage.
- Test across multiple BTC regimes.
- Compare against buy-and-hold BTC and cash/T-bill baseline.
- Report trade count and time out of market.
- Validate on unseen periods before increasing confidence.
