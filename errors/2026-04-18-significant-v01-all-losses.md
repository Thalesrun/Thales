---
date: 2026-04-18 14:29-15:05 ET
severity: significant
market: btc-updown-5m × 6 bars (2:25PM-3:05PM ET)
---

## What happened

Strategy v0.1 first live session: 6 trades, 0 wins, 6 losses. Total loss: $20.53 (13.5% of capital).

| # | Direction | Entry | Cost | Return | P/L | Market |
|---|-----------|-------|------|--------|-----|--------|
| 1 | UP | $0.04 | $3.00 | $0.00 | -$3.00 | 2:25PM |
| 2 | DOWN | $0.40 | $3.00 | $0.00 | -$3.00 | 2:30PM |
| 3 | UP | $0.29 | $2.79 | $0.76 | -$2.03 | 2:45PM |
| 4 | UP | $0.43 | $2.64 | $0.00 | -$2.64 | 2:50PM |
| 5 | UP | $0.19 | $5.32 | $0.00 | -$5.32 | 2:55PM |
| 6 | DOWN | $0.49 | $5.24 | $0.70 | -$4.54 | 3:00PM |

## Why

The v0.1 pricing model (Gaussian random walk + HAR-RV) was fundamentally flawed. It computed its own P(up) estimate and compared against the market price, treating any difference as "edge." In reality, the Polymarket market makers have better models, faster data, and delta-hedging capability. Our model consistently overrode market consensus and was wrong every time.

Specific failures:
1. **No extreme-price filter**: bought at $0.04 (4% implied, pure longshot)
2. **Momentum filter disabled**: bought UP while BTC was actively falling (3 of 5 UP trades)
3. **Mean-reversion bias**: Gaussian model sees any dip as "should revert," but BTC trends persist in 5-min bars
4. **False edge**: model showed +45% edge on trade 1, +42% on trade 5 — these were computational artifacts, not real alpha

Strategy v0.1 has been retired. Replaced by v0.2 (direction-confirmation model) which does not compute its own probability estimate — it follows market direction when auxiliary signals confirm.

→ Corrections: see Learnings #1 (extreme price filter), #2 (momentum filter), #3 (abandon pricing model)
