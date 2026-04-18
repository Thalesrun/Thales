---
date: 2026-04-18 overnight (00:00-08:00 ET)
severity: significant
market: btc-updown-5m × multiple bars overnight
---

## What happened

Overnight the bot ran v0.3 double-buy strategy. When both legs completed (ARB), it was profitable. But many bars only completed LEG1 — buying the cheap side ($0.25-$0.35) without BTC swinging back for LEG2. These single-leg positions settled at $0 approximately 70% of the time (because cheap side = low probability side). 94 positions settled at zero value. Balance dropped from $160 to $117 overnight.

## Why

The v0.3 strategy buys the cheap side first at $3 per leg. "Cheap" means the market says 25-35% probability of winning. When LEG2 doesn't materialize (BTC doesn't swing back), we're left holding a 25-35% probability bet at full size. Over many bars overnight, the 65-75% loss rate on single legs drained the account.

The theoretical math I presented ("long-term profitable") was wrong because:
1. I assumed single legs were 50/50 — they're actually 25-35% (we buy the CHEAP side)
2. I counted ARB wins but underweighted single-leg losses
3. 94 zero-value positions × ~$2 avg = ~$188 total outflow on losers
4. ARB wins couldn't compensate for the volume of single-leg losses

→ Correction: LEG1 reduced to $1 probe. Only scale up to full size ($3) when LEG2 is confirmed. Single-leg max loss reduced from $3 to $1.
