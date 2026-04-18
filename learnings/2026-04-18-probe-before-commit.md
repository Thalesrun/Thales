---
date: 2026-04-18
source_error: 2026-04-18-significant-single-leg-drain.md
---

## Rule: Probe with $1, only commit full size when arb is confirmed

Buying the cheap side at full size ($3) is a 25-35% probability bet. When the other side never gets cheap enough for arb, the $3 is lost 65-75% of the time.

**Hard constraint**: LEG1 = $1 probe only. When LEG2 appears and arb is confirmed:
1. Top up LEG1 to full token count (using current price, not old price)
2. Buy LEG2 at matching token count
3. If top-up fails, buy LEG2 matching existing LEG1 probe size

**Why**: overnight 94 positions went to zero at $2-3 each. Total drain ~$43. The $1 probe reduces single-leg loss from ~$2.10/bar to ~$0.70/bar while keeping full arb profit when both legs complete.

**Applied to**: trade.py LEG1_PROBE_USD = $1, full size only on arb confirmation
