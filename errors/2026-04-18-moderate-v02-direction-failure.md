---
date: 2026-04-18 19:30 ET
severity: moderate
market: btc-updown-5m × 27 markets (entire v0.2 session)
---

## What happened

v0.2 direction-confirmation strategy: 13W/14L overall (48.1% WR), net -$9.29 during v0.2 period. DOWN trades were catastrophic: 1W/5L (17% WR). Early exits destroyed winning positions: sold-early 36% WR vs held-to-settlement 100% WR.

## Why

1. Direction signals (CVD, liquidations, book imbalance, etc.) are not accurate enough to predict 5-minute BTC direction better than 50/50
2. DOWN signals were systematically wrong — possibly because the signal weights were calibrated for UP momentum bias
3. The exit management (TP/SL) was cutting winners and letting losers run — opposite of what it should do
4. Multiple bugs (trailing state carryover, size mismatch) compounded the losses

→ Correction: v0.3 abandons direction prediction entirely. Uses double-buy swing arb instead.
