# Sigma — In-Depth Analysis

*A system-level read of the project as it stands (point-in-time, 2026-07-05): 10 documents, a low-volume manufactured "army × café racer." Analysis, not summary — where it hangs together, where it pulls apart, and what actually determines whether it succeeds. Living document; re-run as the project evolves.*

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
| **Business** — sell as a manufacturer | Repeatability, DfM, supply chains, type-approval, unit economics | **Underdeveloped, unvalidated** |

**The central tension is between spine 2 and spine 3.** The aesthetic and engineering spines are *bespoke by nature* — a featherbed frame, a hand-built ti exhaust, a from-scratch Rust ECU: the language of a one-off passion build, and it's gorgeous. But the business spine demands the **exact opposite** — parts that repeat, labour that scales, a supply chain, and a certified type stamped out under Conformity of Production.

Sigma is simultaneously an **art-bike** and a **production product**, and those pull in opposite directions. The specs caught this once — "harvesting a new donor per bike doesn't scale" — but the finding generalizes: *nearly every bespoke decision that makes Sigma beautiful is a decision that makes it hard to manufacture.* This is the project's defining problem, and it is not yet resolved.

## 3 · System coherence: the cross-domain couplings

The strongest thing about the spec set is that it behaves like a **system, not a parts list.** Decisions propagate across domains and the couplings are tracked, not left dangling:

- **Charging ↔ extreme cooling ↔ climate** — the high-CFM fan is *non-sheddable* and runs hardest at hot idle, exactly when the alternator is weakest; this tightens the marginal charging balance and drives the LiFePO4-buffer / rewound-stator decision.
- **Exhaust O₂ ↔ OBD ↔ for-sale mandate** — the pre/post-cat sensor pair *is* the OBD-II catalyst monitor now legally required; a styling choice that pays a regulatory debt.
- **ABS ↔ Kineo wheel order ↔ critical path** — a tone-ring provision must be specified at the ~18-week long-lead wheel order, so a homologation decision gates a procurement deadline.
- **Gearing ↔ top speed ↔ tire rating ↔ homologation** — closed by the ≤210 km/h target, which keeps the 58H front legal.
- **Exhaust routing ↔ battery/electronics heat** — a genuine conflict, then dissolved by moving to a side-exit.

This traceability is rare and valuable. It's why the project reads as *coherent* despite its breadth: the docs think in interactions, not silos.

## 4 · Risk map

Risks cluster by spine, and their severity is **inverse to how well they're developed:**

- **Technical (well-understood, well-planned).** The custom EFI + safety-critical ride-by-wire is the hardest engineering, but efi.md and the mule runbook de-risk it properly — gated bring-up, fail-safes proven on a bench before an engine start, characterize-don't-invent. The immobiliser and the two-embedded-program reality are named. *Under control on paper.*
- **Business (severe, thin).** Viability rests on **three unvalidated gates**: a Yamaha crate-engine supply deal, design-for-manufacture to cut per-unit labour, and enough volume to amortize a large software NRE within the small-series cap. None proven; any one failing breaks the economics. *The real risk, and the least-developed spine.*
- **Execution (staggering scope).** Bespoke fabrication + two embedded systems + mil-spec electrical + a four-market certification program is realistically **3–4 engineering programs plus a regulatory program plus a business** — for an entity implied to be very small.
- **Regulatory (heavy but correctly mapped).** The pivot to type-approval was handled rigorously; the phased MX→EU/UK→CA→US rollout is sound. Large load, not mis-estimated.

## 5 · The four hard critiques

1. **Scope exceeds plausible capacity.** The engineering is specified to a standard that implies a team; the framing implies very few people. Something must give — team, timeline, or scope.
2. **DfM is flagged, not designed.** "Convert one-off fabrication to jig-repeatable" is a finding, but the frame, swingarm, exhaust, harness and bodywork are still specified bespoke. Manufacturing readiness is an aspiration, not yet an effort.
3. **The custom electronics are both the moat and the millstone.** The from-scratch ECU + cockpit are the genuine differentiator *and* the largest NRE, longest pole, and highest risk. A pragmatic manufacturer would buy a proven standalone ECU — but that erases the identity. This strategic fork (bespoke moat vs. proven pragmatism) is real and **not yet confronted**.
4. **Investment is inverted.** ~90% engineering, ~10% business — but *the business decides success.* Demand, pricing validation, funding and team are barely developed relative to the exhaustive hardware detail.

## 6 · What is genuinely excellent

- **Intellectual honesty** — the docs surface their own hard truths (the noise floor on a short exhaust, the non-scaling donor, the charging tension). Specs that argue against themselves are trustworthy.
- **Identity discipline** — "army × café" is coherent and mostly *emergent* from good prior choices, not bolted on.
- **De-risking method** — mule-first, gated bring-up, cheap-checks-before-expensive-steps is exactly right for the highest-risk subsystem.
- **Regulatory realism** — grounded homologation reasoning, correctly phased.

## 7 · Maturity: where the project actually is

- **Engineering decisions: ~80% locked** — powertrain, chassis, brakes, wheels, suspension, cooling, exhaust, cockpit, electrical standard, ergonomics, ABS, charging.
- **Business / certification: ~20% developed** — economics modeled, rollout phased; viability gates, funding, team, demand and DfM open.
- **Execution: 0%** — no mule bought, no firmware written, no part fabricated.

The gap between the first line and the other two *is* the honest status: **the bike is well-designed; the business and the doing are not yet begun.**

## 8 · Strategic verdict & highest-leverage moves

**As an engineering specification, Sigma is excellent** — coherent, honest, unusually well-integrated. **As a business, it is viable only inside a narrow envelope** (premium boutique pricing, a crate-engine deal, real DfM, volume to carry the software NRE) that is currently unproven.

The highest-leverage next moves are **not** more engineering decisions — they are the things that test the fragile spine:

1. **Validate the crate-engine supply** — one Yamaha conversation that could confirm or kill the unit economics.
2. **Confront the ECU strategic fork** — decide explicitly whether the bespoke electronics are worth being the critical path, or whether a proven ECU + a bespoke *cockpit* captures most of the identity at a fraction of the risk.
3. **Do a real DfM pass** on the top-3 cost/labour drivers (frame, exhaust, harness) — turn the finding into a design.
4. **Buy the mule and start Phase 1 characterization** — the only way to convert paper into evidence; it feeds everything downstream.

**One-line verdict:** *A beautifully coherent motorcycle wrapped around an under-tested business — the engineering is ready to build; the business is not yet ready to bet on, and that, not the hardware, is where the attention now belongs.*
