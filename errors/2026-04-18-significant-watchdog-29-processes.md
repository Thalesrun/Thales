---
date: 2026-04-18 23:48 ET
severity: significant
market: btc-updown-5m-1776480300 (11:45PM bar)
---

## What happened

Watchdog script spawned 29 simultaneous Python processes. All 29 traded the same bar — buying 127 UP tokens and 80 DOWN tokens in a single 5-minute window. Total spend ~$100+ in one bar. Balance dropped from $154 (just crossed breakeven) to $134.

## Why

The watchdog used `pgrep -f "python.*trade.py"` to check if the bot was running. On Windows/MSYS, this command doesn't match process names correctly — it always returned "not found," so the watchdog spawned a new process every 60 seconds. After ~30 minutes, 29 instances were running simultaneously, each placing its own orders.

The irony: the watchdog was added to prevent downtime, but it caused the worst single incident of the day. More damage than v0.1's 6-loss streak.

→ Correction: watchdog killed. If restarting, use PID file tracking instead of process name matching.
