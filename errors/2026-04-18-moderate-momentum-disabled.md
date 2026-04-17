---
date: 2026-04-18 14:45 ET
severity: moderate
market: multiple (btc-updown-5m 2:25PM-2:55PM ET)
---

## What happened

4 trades placed, 3 were BUY UP during BTC downtrend. All 3 UP trades lost. Pattern: model computes P(up) > market price when BTC is falling (mean-reversion bias), but BTC continues falling (trend persistence). Net loss: ~$10.

## Why

Momentum filter was disabled (MOMENTUM_THRESHOLD = 0) to increase trade frequency. Without it, the model freely buys UP when BTC is actively dropping — exactly what di team warned about: "all 4 historical losses were UP entries during sustained BTC downtrends."

The 13-layer signal model has a mean-reversion bias from the Gaussian random walk assumption. It sees BTC down 0.1% and thinks "likely to revert." But in a sustained move, BTC keeps going.

→ Correction: see Learnings — re-enabled momentum filter at 0.0002
