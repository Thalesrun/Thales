---
date: 2026-04-18
source_error: 2026-04-18-significant-watchdog-29-processes.md
---

## Rule: Never deploy untested infrastructure to production

The watchdog script was written and deployed in 30 seconds without any testing. It used a Linux command (pgrep) that doesn't work on Windows. Result: 29 zombie processes, ~$20 loss, wiped out hours of v0.3 profit.

**Hard constraint**: any script that can start processes or place orders MUST be tested in DRY_RUN first. No exceptions.

**Why**: the watchdog was supposed to add reliability but instead caused the single worst incident of the day. Untested "safety" code is more dangerous than no safety code.
