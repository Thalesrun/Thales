---
date: 2026-04-18
source_error: 2026-04-18-moderate-duplicate-orders.md
---

## Rule: Lock traded_this_bar BEFORE placing the order, not after

Setting the bar-lock after order placement creates a race condition: the 100ms signal loop runs multiple times while the order is in-flight (~500ms), resulting in duplicate orders in the same bar.

**Hard constraint**: `state.traded_this_bar = True` must be the FIRST thing that happens when a trade decision is made, before any async order call.

**Why**: 3 duplicate orders in one bar, $7.94 spent instead of $3, and exit_manager only tracked the last order. +109% profit on the combined position went unmanaged and dropped to +16%.
