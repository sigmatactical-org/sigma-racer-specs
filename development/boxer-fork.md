# Sigma — Premise Fork: CP3 Featherbed vs BMW Boxer

*One-page decision spec (2026-07-05). Two coherent premises, different motorcycles. Neither fixes engine supply — both are donor-harvest per unit (no crate engines exist from Yamaha or BMW); the fork is about identity, engineering shape and margins. Dev note, untracked.*

> **DECIDED 2026-07-06: A — stick with the Yamaha CP3.** The boxer strengthened the army story and simplified thermals/electrics, but not enough to justify re-founding half the spec set, +10–15 kg, thinner noise/emissions cert margins, a ~€3–4.5k/unit donor premium, and losing the CP3 standalone community (the ECU program's named de-risk). Spec set stands as written; production supply = new MT-09/XSR900 donor per unit + part-out (see analysis.md §4). Kept below for the record; revisit only if CP3 donor supply itself breaks.

---

## The fork in one line each

- **A · Sigma-CP3** *(spec as written)* — modern **featherbed special, Triton-lineage triple**: liquid-cooled 890 cc screamer in a bespoke chromoly cradle, chain drive, ≤190 kg.
- **B · Sigma-Boxer** — **military-lineage air-cooled twin** (WW2 R75 → M72 → Ural roots): BMW 1170 DOHC boxer as a stressed member under a minimal backbone frame, shaft drive, ~195–205 kg.

## Side by side

| Criterion | A · CP3 featherbed | B · BMW boxer |
|---|---|---|
| Engine | Yamaha CP3 890 cc triple, ~117 hp @ 10k, 93 Nm, liquid-cooled | BMW 1170 DOHC boxer, ~109 hp @ 7k, 115 Nm, air/oil-cooled, Euro 5+ since the 2024 R12 relaunch |
| Character | Revvy café screamer (10.5k redline) | Torquey thumper-twin, engine *is* the styling |
| **Identity fit** | Café: excellent (Triton lineage). Army: styled in | **Army: native** (the archetypal military engine) + café-custom king. Strongest story of any option examined |
| Frame concept | Bespoke featherbed cradle `[BESPOKE]`, radiator packaged inside | Cylinders kill the cradle → **featherbed dies**. Backbone + engine-as-stressed-member; less tube, fewer members |
| Final drive | Chain; gearing is a free decision (locked to ≤210 km/h target) | **Shaft (paralever)**; gearing collapses to BMW bevel-box ratios; bespoke swingarm/linkage/cush-drive rear all rewritten |
| Mass | ≤190 kg wet holds (~55 kg engine allowance) | Realistic **~195–205 kg**; target loosens ~+10–15 kg |
| Cooling | Extreme-cooling program: oversized rad + oil cooler + high-CFM fan + ducting `[BESPOKE]` | **Whole subsystem deleted** — oil cooler only |
| Charging | Marginal at hot idle (non-sheddable fan) → LiFePO4 buffer, maybe rewound stator | **Relaxed** — fan load gone; worst case shrinks ~120–200 W |
| ECU program | 3-cyl sequential; Yamaha immobiliser moderate; **huge CP3 standalone community** (named de-risk) | Engine control *simpler* (2-cyl, conventional Bosch-style hardware; full ECU+loom replacement deletes the keyless/ZFE/coding ecosystem). Risk concentrates in **ABS-Pro CAN integration** (IMU-coupled, expects the BMW bus — the one OEM box that must stay) + **characterization with no standalone community** for the DOHC 1170. Upside to verify: car-style alternator → charging comfortable |
| Emissions/noise cert | Liquid-cooled = stable thermals, proven Euro 5+ base, comfortable margins | Euro 5+ *provable* (BMW does it) but **thinner margins**: air-cooled thermal drift + mechanical noise vs drive-by limit on a custom exhaust |
| Donor cost | MT-09/XSR900 ~€10.5–12k; net engine line **~€7–9k** after part-out | R12 **€14,460** DE list (⚠ 95 hp tune — verify vs nineT's 109 hp: mapping or hardware?); nineT ~€17–18.3k; strong nineT-platform part-out **+ paralever/shaft harvested** (offsets bespoke fab); net **~€10–13k** |
| DfM / manufacturability | Cradle + swingarm + linkage + cooling = heavy bespoke load | **Better**: minimal frame, no radiator packaging, fewer bespoke members |
| Spec impact | Zero — nine docs stand | **~Half the spec set rewritten**: chassis, engine, bodywork stance, chunks of electronics/build; efi.md architecture survives |

## Invariant either way

Donor-harvest + part-out pipeline · both embedded programs (ECU + cockpit) · mil-spec loom · homologation program & MX→EU/UK→CA→US rollout · mule-first gated bring-up · premium boutique pricing.

## Decision drivers

**Pick A (CP3)** if: the ≤190 kg / chain / revvy-café DNA is the product; cheapest donor and friendliest ECU target; zero spec churn; ship the bike already designed.

**Pick B (Boxer)** if: the *army* half of the identity is the soul of the product; deleting cooling/charging complexity and shrinking bespoke fabrication is worth +10–15 kg, shaft drive, a pricier donor and thinner cert margins.

## Cheap checks before any pivot (timebox alongside supply validation)

1. R12 donor teardown facts: clutch actuation type, true engine+box+shaft mass, loose-harvest feasibility of the paralever.
1b. **R12 (95 hp) vs R12 nineT (109 hp) delta — calibration-only or hardware (cams/intake)?** Decides whether the €14,460 base R12 or the ~€17–18k nineT is the real donor (~€3k/unit swing).
2. Immobiliser/CAN reality: can the DOHC 1170 run standalone? (community + bench-sniff evidence, per the mule method).
3. Noise margin: any data on aftermarket R12 exhausts passing EU drive-by.
4. Kineo (or equal) wheel fitment for the paralever rear.
5. Donor price + nineT part-out values, EU market.

## Recommendation

**Hold A unless the identity pull is decisive.** B is the only alternative examined that *strengthens* the story while *simplifying* engineering — but it re-founds the project and thins the two hardest certification margins (noise, emissions). If B stays alive after the five checks, decide before the mule buy (T0, Sep 2026) — the mule is engine-specific and starts the clock on whichever premise it embodies.
