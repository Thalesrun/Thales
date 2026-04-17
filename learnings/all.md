# 经验沉淀

每条必须挂钩至少一个 errors/ 条目。先验规则归 strategy/current.md。

---

## 1. Don't trade against extreme market consensus (2026-04-18)

When Polymarket prices a token at < $0.10 or > $0.90, skip the trade. The model's P(up) estimate is not accurate enough to override 90%+ market conviction.

- Source error: `errors/2026-04-18-significant-first-live-loss.md`
- Hard constraint: skip if `ask < 0.10` or `ask > 0.90`
- Applied to: `strategy/signal.py` signal filter

## 2. Never disable momentum filter (2026-04-18)

Buying UP requires BTC 10-second momentum ≥ +0.0002; buying DOWN requires ≤ -0.0002. Without this, the model trades against strong trends and loses systematically.

- Source error: `errors/2026-04-18-moderate-momentum-disabled.md`
- Hard constraint: MOMENTUM_THRESHOLD > 0 (at least 0.0002)
- Applied to: `config.py` MOMENTUM_THRESHOLD

## 3. Don't predict direction — arb is safer than guessing (2026-04-18)

v0.2 tried to predict direction using 12 signals: 48% WR, not profitable. DOWN was 17% WR. Instead of improving prediction, switch to mechanical arb (double-buy swing) that doesn't require being right about direction.

- Source error: `errors/2026-04-18-moderate-v02-direction-failure.md`
- Applied to: strategy rewrite v0.2 → v0.3

## 4. Don't compute your own probability to override the market (2026-04-18)

The market price IS the best probability estimate. Our Gaussian model was less accurate than MMs. "Edge" was a modeling artifact. v0.1 retired (0W/6L, -$20.53). Replaced by v0.2 direction-confirmation.

- Source error: `errors/2026-04-18-significant-v01-all-losses.md`
- Hard constraint: never trade "my P(up) > market P(up)"
- Applied to: strategy rewrite v0.1 → v0.2
