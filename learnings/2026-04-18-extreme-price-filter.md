---
date: 2026-04-18
source_error: 2026-04-18-significant-first-live-loss.md
---

## Rule: Don't trade against extreme market consensus

When Polymarket prices a token at < $0.10 or > $0.90, the market is saying 90%+ probability in one direction. The model's P(up) estimate based on HAR-RV is not accurate enough to override that level of market conviction.

**Hard constraint**: skip the trade if `ask < 0.10` (buying a 10% longshot) or `ask > 0.90` (paying 90 cents for a near-certainty with tiny upside).

**Why**: First live trade bought UP @ $0.04. Model said 50% edge. Market was right, model was wrong. $3 lost. The model doesn't capture intra-bar momentum well enough to bet against 96% market consensus.
