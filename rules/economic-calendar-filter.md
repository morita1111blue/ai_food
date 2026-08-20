---
date: 2026-08-20
source_project: codex-cross-thread/economic-news-automation
status: rule
confidence: high
---

# Economic Calendar Filter

## Rule

Market event notifications should separate broad awareness from calendar-grade commitments.

Use the thread notification for broad market context, but add Google Calendar events only when the event is both time-sensitive and likely to move positions or watchlists. If the impact is unclear, do not add it.

## Calendar-worthy events

- Central bank decisions: FOMC, BOJ, ECB, BOE policy decisions and press conferences.
- Major inflation and labor data: CPI, PCE, NFP, unemployment rate, average hourly earnings.
- Major growth/activity data: GDP, flash PMI, ISM, US retail sales.
- Major fiscal or government events with market timing impact.
- Very high-impact earnings for mega-cap, AI, semiconductor, memory, cloud, finance, or Japan index-heavy names.

## Usually exclude

- Normal housing data.
- Regional Fed indices.
- Wholesale inventories.
- Trade balance.
- Market holidays or exchange closures unless they change a trading plan.
- Low or medium importance indicators.
- Already released items.
- Events without a reliable timestamp.
- General market themes that do not belong on a calendar.

## Earnings filter

Research earnings broadly, but add only the ones with clear timing and high market impact.

Typical candidates include Nvidia, Microsoft, Alphabet, Amazon, Meta, Apple, Tesla, TSMC, ASML, Samsung, SK hynix, Micron, JPMorgan, Toyota, SoftBank Group, and Tokyo Electron.

## Calendar event format

- Economic indicator: `経済指標: 米・CPI`
- Central bank or policy event: `経済イベント: FOMC政策金利`
- Earnings: `決算: Nvidia`

Use Asia/Bangkok as the display timezone when the user's operating context is Thailand time.

## Failure handling

Calendar writes are helpful but non-critical. If a calendar API call fails, continue the research/reporting flow and clearly state which events were not added.
