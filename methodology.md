# BraidForecast AI — Methodology (BraidConsumption Engine)

**Plain-language explainer for a non-technical investor. The rule structure below is fully public — no hidden weights.**

## 1. The problem

Braiders run out of hair mid-appointment or over-buy stock because nothing connects the appointment book to hair inventory. A single install can consume 6–10+ packs across 250+ colors × brands × lengths, and 2025–26 tariffs on Chinese-sourced synthetic braiding hair are actively raising per-pack costs, squeezing already-thin margins.

## 2. Inputs

The engine takes what a stylist already knows about the appointment:

- Service type (knotless / box braids / feed-in / crochet / twists)
- Braid size (1x–4x) and length (short / medium / waist / hip)
- Fullness / density (1–5)
- Color mix (single / multi / blend code, e.g. "1B/30")
- Brand and pack size (e.g. 33g, 48g, 64g)
- Stretch factor (1x–4x)
- Stylist calibration history (device-local)

## 3. The decision rules (public)

1. **Packs-per-style lookup** — base packs by service: Knotless 6 · Box 5 · Feed-in 4 · Crochet 3 · Twists 4.
2. **Density multiplier** — `0.7 + (density × 0.15)`; denser styles pull more packs.
3. **Length multiplier** — Short 0.8 · Medium 1.0 · Waist 1.25 · Hip 1.45.
4. **Braid-size multiplier** — `1.3 − (size × 0.1)`; smaller braids use more packs.
5. **Waste factor** — fixed +8%.
6. **Partial-pack carryover** — fractional packs round up to the nearest whole pack for purchasing, with carryover tracked against the next appointment.
7. **Calibration** — a per-stylist multiplier learned from "actual packs used" feedback, stored locally on that stylist's device only.

Output is a range (e.g. "6–8 packs") with a one-line reason code explaining what drove it (e.g. "knotless + 3x density + 2-color mix"), a per-color reserve list, a confidence %, and an estimated wholesale cost range.

## 4. Calibration

After each completed service, the stylist enters actual packs used. The engine compares actual vs. predicted and nudges a per-stylist multiplier (bounded, e.g. 0.6–1.6x) that shifts the next prediction. This is **device-local** — no cloud account, no forced sign-up, no data leaves the stylist's device.

## 5. Confidence scoring

Confidence starts near 58–65% on the public formula alone and rises as a stylist enters real feedback after appointments — each data point tightens the calibration multiplier for that stylist specifically.

## 6. Limitations

The engine **supports purchasing decisions, not a promise**. It does not guarantee exact usage, does not replace a stylist's professional judgment, and is not yet validated against a large real-world dataset. Treat every number as a purchasing aid.

## 7. Confidentiality

The rule structure above is public. Per-stylist accumulated data and any optimized weights remain confidential and are not exposed publicly.
