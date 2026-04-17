---
date: 2026-04-18 16:12 ET
severity: moderate
market: Bitcoin Up or Down - April 17, 4:10PM-4:15PM ET
---

## What happened

3 orders placed in the same 5-min bar ($2.39 + $2.55 + $3.00 = $7.94 total, should be max $3). Position reached +109% unrealized profit but TP only tracked the last order. Earlier orders were unmanaged. Profit dropped from +$8.33 to +$0.86 as BTC reversed.

## Why

`traded_this_bar = True` was set AFTER the order was placed. The signal loop runs every 100ms but order placement takes ~500ms. Multiple iterations slipped through before the lock was set. Also, `active_trade` only stored the last order, so exit_manager couldn't TP the full position.

→ Correction: moved lock to BEFORE order placement. Now impossible to double-order in same bar.
