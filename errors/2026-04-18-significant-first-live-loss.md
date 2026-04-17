---
date: 2026-04-18 14:29 ET
severity: moderate
market: Bitcoin Up or Down - April 17, 2:25PM-2:30PM ET (btc-updown-5m-1776450300)
---

## What happened

First live trade. Bought UP 69.8 tokens @ $0.04 = $3.00. BTC was falling hard during the bar — market priced UP at 4% probability. Model calculated P(up) ≈ 50%, saw +45% "edge", and bought. BTC continued falling. UP lost. Token went to $0. Lost $3.00.

## Why

The model's P(up) was wildly disconnected from reality. At $0.04 market price, BTC had already dropped significantly within the bar. The HAR-RV model uses bar-open price as reference and computes probability from a Gaussian random walk — but it doesn't account for strong intra-bar momentum. The "45% edge" was an illusion: the model said 50/50 while the market (correctly) said 96% DOWN.

Root cause: MIN_EDGE threshold is too low (0.5%) and the model lacks a filter for extreme market prices. When market says 4% and model says 50%, the model is almost certainly wrong, not the market.

→ Correction: see Learnings
