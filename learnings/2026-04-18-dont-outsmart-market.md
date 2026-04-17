---
date: 2026-04-18
source_error: 2026-04-18-significant-v01-all-losses.md
---

## Rule: Don't compute your own probability to override the market

The Polymarket market price IS the best available estimate of outcome probability. A HAR-RV Gaussian model cannot outperform market makers who have better data, faster infrastructure, and hedging capabilities.

**Hard constraint**: never trade based on "my P(up) > market P(up)." Instead, treat market price as ground truth and only trade when directional signals (CVD, liquidations, order flow, cross-asset) confirm the trend.

**Why**: v0.1 computed its own P(up), found "edge" everywhere, and lost every trade. 0W/6L, -$20.53. The "edge" was a modeling artifact. Replaced by v0.2 direction-confirmation approach.
