# Sigma — In-Depth Analysis

*A system-level read of the project as it stands (point-in-time, 2026-07-05, re-run after the crate-engine supply validation): nine spec files + dev notes, a low-volume manufactured "army × café racer." Analysis, not summary — where it hangs together, where it pulls apart, and what actually determines whether it succeeds. Living document; re-run as the project evolves.*

---

## 1 · The thesis: what Sigma has become

Sigma started as a flat-black café racer and has evolved into something far more specific and demanding: **a premium, blacked-out, mil-spec "army × café" motorcycle, engineered bespoke from the frame up — including two ground-up embedded computers — and intended for sale as a low-volume manufactured product across four regulatory regimes.**

That single sentence contains the whole story, because it names three ambitions that each would be a serious undertaking alone, and Sigma is attempting all three at once. Understanding the project means understanding how those ambitions reinforce — and fight — each other.

## 2 · The three spines — and the central tension

Every decision serves one of three "spines," and coherence depends on their alignment:

| Spine | What it demands | State |
|---|---|---|
| **Aesthetic** — army × café | Restraint, blackout, tactical minimalism, mil-spec ruggedness | **Coherent, largely emergent** |
| **Engineering** — bespoke everything | Custom chassis + custom EFI + Linux cockpit + mil-spec loom | **Deep, ambitious, well-specified** |
| **Business** — sell as a manufacturer | Repeatability, DfM, supply chains, type-approval, unit economics | **Underdeveloped — and the first gate tested came back at-risk** |

**The central tension is between spine 2 and spine 3.** The aesthetic and engineering spines are *bespoke by nature* — a featherbed frame, a hand-built ti exhaust, a from-scratch Rust ECU: the language of a one-off passion build, and it's gorgeous. But the business spine demands the **exact opposite** — parts that repeat, labour that scales, a supply chain, and a certified type stamped out under Conformity of Production.

Sigma is simultaneously an **art-bike** and a **production product**, and those pull in opposite directions. *Nearly every bespoke decision that makes Sigma beautiful is a decision that makes it hard to manufacture.* This remains the project's defining problem — and as of this month it is no longer abstract: the first supply-chain test (§4) returned evidence on the business spine's side of the ledger, and it was bad news.

## 3 · System coherence: the cross-domain couplings

The strongest thing about the spec set is that it behaves like a **system, not a parts list.** Decisions propagate across domains and the couplings are tracked, not left dangling:

- **Charging ↔ extreme cooling ↔ climate** — the high-CFM fan is *non-sheddable* and runs hardest at hot idle, exactly when the alternator is weakest; this tightens the marginal charging balance and drives the LiFePO4-buffer / rewound-stator decision.
- **Exhaust O₂ ↔ OBD ↔ for-sale mandate** — the pre/post-cat sensor pair *is* the OBD-II catalyst monitor now legally required; a styling choice that pays a regulatory debt.
- **ABS ↔ Kineo wheel order ↔ critical path** — a tone-ring provision must be specified at the ~18-week long-lead wheel order, so a homologation decision gates a procurement deadline.
- **Gearing ↔ top speed ↔ tire rating ↔ homologation** — closed by the ≤210 km/h target, which keeps the 58H front legal.
- **Exhaust routing ↔ battery/electronics heat** — a genuine conflict, then dissolved by moving to a side-exit.
- **Engine supply ↔ everything** — newly visible (§4): the CP3 choice is upstream of the firmware NRE, the frame, the ABS, the charging design and the ancillary sourcing rule; its supply chain is the one coupling that was assumed rather than designed.

This traceability is rare and valuable. It's why the project reads as *coherent* despite its breadth: the docs think in interactions, not silos.

## 4 · The engine-supply finding — the new centre of gravity

The July validation (`build.md` §2d, `engine.md` §1) is the most consequential fact to enter the project since the for-sale pivot:

**No Yamaha CP3 crate supply exists.** Yamaha keeps the CP3 in-house — no public crate program, no known third-party channel. The two live leads are **TKRP (NL)** complete R9/CP3 race-spare engines and a direct **Yamaha Motor Europe OEM-supply negotiation** (volume-committed, uncertain appetite). Until one lands, the production engine line is the whole-donor fallback: buy a ~$10k MT-09 per unit and surplus most of it.

Three things make this bigger than a sourcing annoyance:

1. **Everything downstream is CP3-specific.** The trigger characterization, sensor transfer functions, ride-by-wire throttle-body control, immobiliser handshake, ABS CAN integration, charging design, engine mounts and frame packaging are all built to this engine. The firmware *architecture* (decoder, safety monitor, fault matrix) would port; the calibration, characterization and mechanical design would not. An engine substitution after heavy firmware and tooling spend is close to a full reset — which is why the spec's own rule ("resolve before tooling/type-approval spend") is right, and arguably should extend to the new-donor buy at T0+6–9.
2. **Even a successful crate deal only half-solves it.** The "Yamaha-first ancillaries" economics assume a *whole donor*: the ABS modulator + tone rings, radiator + fan, in-tank pump, stator + reg/rec come with the bike, "already paid for." A crate engine covers at best the engine/gearbox/throttle-body core — the ancillary BOM must be re-sourced and re-priced either way. The spec has not yet costed this.
3. **The Mexico pilot's purpose partially evaporates.** Phase 1 was meant to "prove crate-engine supply" among other things; there is currently no crate supply to prove. Donor-harvest is fine for the first few units, so the pilot can still run — but it now proves production and demand, not the engine line.

**One mitigation the spec hasn't considered:** the whole-donor fallback is priced as pure surplus, but a stripped MT-09 leaves a saleable rolling chassis' worth of parts (suspension, wheels, bodywork, electronics). Systematic part-out recovery could claw back a meaningful slice per unit and soften the fallback COGS. Worth a line in `build.md` §2d if the fallback becomes the base case.

To the project's credit, the finding is recorded honestly, cross-referenced in three places, and carries an explicit decision rule. That is exactly how a negative result should be handled — but a well-documented open risk is still open.

## 5 · Risk map

Risks cluster by spine, and their severity is **inverse to how well they're developed:**

- **Technical (well-understood, well-planned).** The custom EFI + safety-critical ride-by-wire is the hardest engineering, but efi.md and the mule runbook de-risk it properly — gated bring-up, fail-safes proven on a bench before an engine start, characterize-don't-invent. *Under control on paper.*
- **Business (severe — now partially evidence-backed).** Viability rests on three gates: crate-engine supply, design-for-manufacture, and volume-to-amortize-NRE within the small-series cap. **Gate one has now been tested and returned at-risk (§4); gates two and three remain untested.** The spine most likely to kill the project is the one where the only evidence so far points the wrong way.
- **Execution (staggering scope).** Bespoke fabrication + two embedded systems + mil-spec electrical + a four-market certification program is realistically **3–4 engineering programs plus a regulatory program plus a business** — for an entity implied to be very small.
- **Regulatory (heavy but correctly mapped).** The pivot to type-approval was handled rigorously; the phased MX→EU/UK→CA→US rollout is sound. Large load, not mis-estimated.

## 6 · The four hard critiques

1. **Scope exceeds plausible capacity.** The engineering is specified to a standard that implies a team; the framing implies very few people. Something must give — team, timeline, or scope.
2. **A `[LOCKED]` engine rests on an unconfirmed supply chain.** The CP3 is the most locked decision in the project — and the only one whose production supply has been checked and found wanting. The spec carries the right hedge ("reconsider the engine or the premise"), but every week of CP3-specific work deepens the commitment while the supply question stays open. Timebox it.
3. **The custom electronics are both the moat and the millstone.** The from-scratch ECU + cockpit are the genuine differentiator *and* the largest NRE, longest pole, and highest risk — and their CP3-specificity now compounds the supply risk (§4). The strategic fork (bespoke moat vs. proven standalone ECU + bespoke cockpit) is real and **still not confronted**; the supply finding makes confronting it more urgent, not less.
4. **DfM is flagged, not designed.** "Convert one-off fabrication to jig-repeatable" is a finding, but the frame, swingarm, exhaust, harness and bodywork are still specified bespoke. Manufacturing readiness is an aspiration, not yet an effort — gate two of three, untested.

## 7 · What is genuinely excellent

- **Intellectual honesty** — the docs surface their own hard truths (the noise floor on a short exhaust, the charging tension), and now demonstrably *act* on them: the crate-supply gate was named, tested, and the negative result recorded with a decision rule rather than buried. Specs that argue against themselves are trustworthy.
- **Identity discipline** — "army × café" is coherent and mostly *emergent* from good prior choices, not bolted on.
- **De-risking method** — mule-first, gated bring-up, cheap-checks-before-expensive-steps is exactly right for the highest-risk subsystem, and the same method is now being applied to the business gates.
- **Regulatory realism** — grounded homologation reasoning, correctly phased.

## 8 · Maturity: where the project actually is

- **Engineering decisions: ~80% locked** — powertrain, chassis, brakes, wheels, suspension, cooling, exhaust, cockpit, electrical standard, ergonomics, ABS, charging.
- **Business / certification: ~25% developed** — economics modeled, rollout phased, and **validation has begun**: one of three viability gates tested (result: at-risk). Funding, team, demand, DfM and the remaining two gates open.
- **Execution: software well underway, hardware 0%** *(corrected 2026-07-06 — the earlier "0%" was wrong)*. The mule (new XSR900 GP) is on order. The EFI firmware exists (`sigma-racer-efi`: engine-agnostic core + CP3 profile, 24 host tests green, targeting the **bought microRusEFI board** — which quietly resolves critique 3's strategic fork: proven hardware, bespoke firmware). The cockpit program is further still: Yocto/RAUC cluster layer (`sigma-racer-wingman`), M7 Embassy safety firmware (`cafe-racer-sidearm`), telemetry + a shared CAN-dictionary crate (`sigma-instrumentation`), and two published support libraries (`dbc-rs`, `mdf4-rs`). Still missing from EFI M0: the trigger decoder, angle-domain scheduler, and the RbW safety monitor + fault matrix — the safety-critical core. No part fabricated.

The honest status: **the bike is well-designed, the software programs are genuinely moving, and the remaining zeros are fabrication, the business gates (DfM, demand), and the safety-critical firmware core.**

## 9 · Strategic verdict & highest-leverage moves

**As an engineering specification, Sigma is excellent** — coherent, honest, unusually well-integrated. **As a business, it is viable only inside a narrow envelope** (premium boutique pricing, an engine supply deal, real DfM, volume to carry the software NRE) — and the first probe of that envelope found its most load-bearing wall unconfirmed.

The highest-leverage next moves, in order:

1. **Drive the engine-supply question to a decision, with a deadline.** The desk validation is done; now run the two leads — a TKRP quote (price, spec, what the "complete engine" actually includes) and a Yamaha Motor Europe conversation — to a yes/no **before the new-donor buy (T0+6–9), and ideally before T0**. Define the kill/pivot rule now: if no deal, is the answer donor-harvest-with-part-out at lower volume, a different engine, or a narrower premise? The used mule (~cheap, architecture-portable) is acceptable spend either way; the new donor and tooling are not.
2. **Confront the ECU strategic fork** — decide explicitly whether the bespoke, CP3-specific electronics are worth being both the critical path *and* a multiplier on the supply risk, or whether a proven ECU + a bespoke *cockpit* captures most of the identity at a fraction of the exposure.
3. **Price the fallback honestly.** Rework `build.md` §2c/§2d with whole-donor + part-out recovery as the *base case* and crate supply as the upside — if the economics only close on an unconfirmed deal, that's the real finding.
4. **Do a real DfM pass** on the top-3 cost/labour drivers (frame, exhaust, harness) — test gate two the way gate one was tested.
5. **Buy the mule and start Phase 1 characterization** at T0 — the only way to convert paper into evidence; it feeds everything downstream and stays cheap enough to survive an engine pivot.

**One-line verdict:** *A beautifully coherent motorcycle wrapped around a business that has just produced its first hard evidence — and the evidence says the engine line, not the engineering, is the wall to resolve before another dollar of CP3-specific commitment.*
