---
date: 2026-04-18 15:22 ET
severity: significant
market: Bitcoin Up or Down - April 17, 3:20PM-3:25PM ET (btc-updown-5m-1776453600)
---

## What happened

Bought DOWN @ $0.41 (6 tokens, $2.46). Price rose to $0.745, unrealized profit +$2.01 (+81.7%). Take-profit threshold was $0.738 (1.8× entry). Price exceeded TP but the position was NOT sold. Profit evaporated.

## Why

The trading bot crashed due to `ImportError: cannot import name 'compute_p_up'` in status_loop. This was a leftover reference to the v0.1 pricing function that was removed in the v0.2 rewrite. The crash killed the entire asyncio event loop, including the exit_manager task. With no exit_manager running, the TP trigger at $0.738 was never checked, and $2.01 unrealized profit was lost.

Root cause: code quality — didn't test that all modules were updated after the v0.1→v0.2 rewrite before going live. A single import error in a non-critical module (status logging) brought down the entire bot including critical modules (exit manager, order placement).

→ Correction: see Learnings — isolate tasks so one crash doesn't kill everything; always DRY_RUN test after any code change
