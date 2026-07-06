# Sigma — Cost & Manufacturer Economics (INTERNAL)

*Moved out of `build.md` §2 (2026-07-06) — the specs repo is public and feeds the public specs page via the info service; the money does not belong there. This is the working copy: COGS, NRE, pricing, breakeven and the business-model findings. Update here; `build.md` keeps a stub pointer.*

*Rough order-of-magnitude estimates — USD, ranges not quotes. As a **low-volume manufacturer** the model is **NRE (one-time) + per-unit COGS × volume**. Both are built out below. Numbers are planning figures per the project rule — confirm on quote.*

## 2a · Per-unit parts/materials (production parts only)

*Excludes the NRE items — the mule (XSR900 GP), dev boards (EVK) and tooling live in §2b, not per bike.*

| Bucket | Includes | Est. (USD) |
|---|---|---|
| Powertrain | CP3 engine (crate/supply — see finding 1; or ~$9–11k whole donor) + ti exhaust + cooling + covers (`engine.md`) | **$12–16k** |
| Chassis / suspension / brakes | Öhlins FG 621 + STX 46 + Kineo pair + Brembo f+r + bearings/chain/tires (`chassis.md`) | **$11–12k** |
| Electronics / cockpit | ECU BOM + Toradex Verdin SoM + bespoke carrier + display + cameras/modem + wideband (`electronics.md`) | **$2–3k** |
| Electrical / harness | Loom + fuse/relay box + LiFePO4 + LED lighting + switchgear (`electrical.md`) | **$2–2.5k** |
| Bodywork | Bespoke tank + seat/cowl + clip-ons/rearsets + controls (`bodywork.md`) | **$4–5k** |
| Fabrication | Frame, swingarm, yokes, stem, axle, brackets — **materials + machining** | **$3–6k** |
| **Per-unit parts subtotal** | | **~$34–45k** |
| **+ Assembly/fab/tune labour** | ~150–300 h bespoke @ shop rate | **~$10–18k** |
| **≈ Per-unit COGS** | | **~$45–65k** |

## 2b · NRE (one-time, volume-independent)

| Item | Est. (USD) | Note |
|---|---|---|
| **ECU firmware program** | *person-years* / founder time | Rust/Embassy + OBD + safety case (`efi.md`) — the single biggest sunk effort |
| **Cockpit Linux program** | *person-years* / founder time | BSP + maps/cameras/HMI + M7 safety fw (`electronics.md` §8) |
| Homologation / type-approval | ~$30–100k+ | EU/UK/CA/MX small-series program (`emissions_certification.md`) |
| Prototyping | ~$15–30k | Mule + benches + dev boards (see the ECU-on-mule dev runbook) |
| Tooling / jigs / fixtures | ~$10–40k | Frame jig + repeatable fab fixtures for production |
| **NRE (cash, ex-software-labour)** | **~$55–170k+** | **Dominated by the two software programs if that labour is paid rather than founder time** |

## 2c · Unit economics & volume

- **Small-series caps:** EU small-series type-approval limits annual volume **per type** — realistically **~10–50/yr** for a bespoke builder. Confirm the current cap; exceeding it forces full type-approval.
- **Pricing:** to work at this COGS, retail must be **premium — ~$80–130k+** (boutique/bespoke tier, not mass-market).
- **Breakeven:** NRE ÷ per-unit contribution margin. e.g. ~$300k effective NRE ÷ (~$95k price − ~$60k COGS ≈ $35k margin) ≈ **~9 units to clear NRE**, then profit — but *highly* sensitive to price, COGS, and whether software is paid labour or founder time.

## 2d · Business-model findings (the hard truths)

1. **Harvesting a new donor per bike doesn't scale.** Buying a whole ~$10k MT-09 just to harvest one engine, per unit, is brutal — the rest is surplus. A manufacturer needs a **Yamaha crate-engine / OEM supply arrangement**, or the engine line alone wrecks the margin. *(Reframes `engine.md`'s "buy new donor" for production.)* **⚠ Validated at-risk (2026-07):** no public Yamaha CP3 crate program exists (Yamaha keeps the CP3 in-house). Nearest leads — TKRP complete R9/CP3 race-spare engines (NL), or a direct Yamaha OEM-supply deal (uncertain). **Crate supply is unconfirmed — carry a whole-donor pricing fallback until a deal is signed; if none lands, reconsider the engine or the premise before tooling spend.** *(2026-07-06: donor-harvest + part-out accepted as the base case — see `analysis.md` §4; net engine line ~€7–9k/unit after ~€2–4k takeoff recovery.)*
2. **Software NRE dominates and fights low volume.** Two full embedded programs are a fixed sunk cost that *demands* volume to amortize — in direct tension with "low-volume / small-series."
3. **Design-for-manufacture becomes mandatory.** Bespoke-everything + ~200 h/bike won't scale; convert one-off fabrication (frame, swingarm, yokes) to **jig-repeatable** production or per-unit labour stays high.
4. **Position premium boutique.** At ~$45–65k COGS the only viable market is the **$80–130k+ bespoke tier**, competing on craft + tech, not price.

**Bottom line:** viable **only** as a premium boutique manufacturer with (a) a solved **engine line** (donor-harvest + part-out is the base case; crate supply is upside), (b) **design-for-manufacture** to cut per-unit labour, and (c) enough volume **within the small-series cap** to amortize a large software NRE. Confirm all three before committing tooling / type-approval spend.
