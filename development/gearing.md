# Sigma — Final-Drive Gearing Calculation

*Dev note (2026-07-07). Closes the `chassis.md` gearing `[PENDING]` with verified numbers. Sources: gear ratios + 16/45 final from the official 2024 MT-09 owner's manual (BME-28199-20, §11 specifications); primary reduction 1.681 (79/47) cross-checked against the Yamaha manual spec page. Tire: locked 170/60-17 STR (OD 635.8 mm, rolling circ. 1.997 m — +0.95 % vs the donor's 180/55).*

## Verified drivetrain (gen-3 CP3)

| Stage | Ratio |
|---|---|
| Primary reduction | **1.681** (79/47) |
| 1st–6th | 2.571 · 1.947 · 1.619 · 1.381 · 1.190 · **1.037** |
| Stock final | 16/45 = 2.8125 (525 chain) |

## Candidates on the 170/60-17

| Final (520) | Theoretical 6th @ 10,500 | rpm @ 210 km/h (6th) | rpm @ 130 km/h cruise | 1st @ redline |
|---|---|---|---|---|
| **16/45 (stock ratio)** | **256.7 km/h** | **8,591** | **5,318** | 103.5 km/h |
| 16/46 | 251.1 | 8,782 | 5,436 | 101.3 |
| 16/47 | 245.7 | 8,973 | 5,555 | 99.1 |
| 15/45 | 240.6 | 9,164 | 5,673 | 97.1 |

## The finding

**Gearing alone cannot honor the ≤210 km/h ceiling.** Capping the *theoretical* 6th-gear top speed at 210 needs a final around 3.44 (16/55) — which puts a 130 km/h cruise at ~6,500 rpm: buzzy, anti-café, and it wrecks the touring character for a constraint the engine never reaches anyway (the CP3 is drag-limited near 210–215 in practice).

**The right instrument is the one we own: the ECU.** Sigma's ride-by-wire means a **firmware top-speed limiter at 210 km/h** is a calibration line, not a component — the declared top speed for homologation is enforced electronically (exactly how OEMs resolve tire-rating ceilings), the 58H front stays legal, and the gearing is freed to serve the riding.

## Decision (proposed → lock in chassis.md)

- **Final drive 16/45 in 520 pitch** — the donor's ratio, proven on this exact engine/mass class; relaxed 5.3k cruise at 130 km/h; the 520 conversion was already locked for lightness.
- **Firmware speed limiter: 210 km/h declared** (`efi.md` — RbW torque cap above threshold; homologation declares the limited value; ties the tire-rating checklist item closed).
- Kineo Ergal carrier ordered for a **520 rear sprocket, 45T aluminium** (steel optional for service life).
- Speedo source: front wheel-speed (ABS sensor) — immune to sprocket swaps.

*(If road testing wants more snap, one tooth at the rear (16/46) costs 6 % cruise rpm — the carrier makes sprocket experiments cheap. The tire's +1 % diameter vs donor is absorbed in calibration.)*
