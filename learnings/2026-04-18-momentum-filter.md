---
date: 2026-04-18
source_error: 2026-04-18-moderate-momentum-disabled.md
---

## Rule: Never disable momentum filter

The momentum gate (MOMENTUM_THRESHOLD > 0) prevents buying UP when BTC is actively falling and buying DOWN when BTC is actively rising. Disabling it causes the model to trade against strong trends, resulting in systematic losses.

**Hard constraint**: MOMENTUM_THRESHOLD must be > 0 (at least 0.0002). Buying UP requires BTC 10-second momentum ≥ +0.0002; buying DOWN requires ≤ -0.0002.

**Why**: 3 consecutive losses from buying UP during a BTC downtrend. The Gaussian model has mean-reversion bias — it sees a dip and thinks "revert." Momentum filter forces the model to only trade WITH the short-term direction, not against it.
