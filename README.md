# BraidForecast AI — BraidConsumption Engine

Public algorithm demo + methodology for BraidForecast AI, a product by **Bennett AI Solutions Inc.**

BraidConsumption predicts how many packs of braiding hair an appointment will consume, so braiders stop running out mid-service and stop tying up cash in over-stocked shelves.

## Live

- **Interactive simulator**: https://jamestown502502.github.io/braidforecast-algorithm/
- **Algorithm demo (transparent rules)**: https://jamestown502502.github.io/braidforecast-algorithm/algorithm.html
- **Methodology (plain-language)**: [methodology.md](methodology.md)

## What's in this repo

| File | Purpose |
|---|---|
| `index.html` | Interactive simulator — picks a prediction from stylist preset, service, size, length, density, color mix; shows packs range, per-color reserve list, confidence %, wholesale cost, public rules, and device-local recalibration from "actual packs used" |
| `algorithm.html` | Transparent algorithm demo — the public formula (packs-per-style, density/length/size multipliers, waste factor), confidence scoring, and what the engine does NOT do |
| `methodology.md` | Plain-language methodology for non-technical investors |

## The public formula (no hidden weights)

```
packs = base(service) × density(0.7 + d×0.15) × length(0.8–1.45) × size(1.3 − s×0.1) × waste(1.08) × calibration
```

- Base packs: Knotless 6 · Box 5 · Feed-in 4 · Crochet 3 · Twists 4
- Calibration: per-stylist multiplier learned from actual-packs-used feedback, stored locally on the stylist's device
- Confidential: per-stylist data and any optimized weights are never exposed

**Estimates support purchasing decisions; final stock is the stylist's call.** Not a guarantee, not validated against a large real-world dataset.

© Bennett AI Solutions Inc. · jb@bennettaisolutions.tech
