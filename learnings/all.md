# 经验沉淀

每条必须挂钩至少一个 errors/ 条目。先验规则归 strategy/current.md。

---

## 1. Don't trade against extreme market consensus (2026-04-18)

When Polymarket prices a token at < $0.10 or > $0.90, skip the trade. The model's P(up) estimate is not accurate enough to override 90%+ market conviction.

- Source error: `errors/2026-04-18-significant-first-live-loss.md`
- Hard constraint: skip if `ask < 0.10` or `ask > 0.90`
- Applied to: `strategy/signal.py` signal filter
