# Sigma — Phased Product Approach

*Dev note (2026-07-06). The product-evolution roadmap: three steps from the XSR900 GP platform to the for-sale Sigma. This sequences the **vehicle**; the ECU program (mule runbook) runs in parallel on the same GP and is gated independently. `build.md` §4 build phases nest inside Steps 2–3.*

---

## Step 1 · Front end, wheels, tires — on the GP, original triple clamps

*Prove the running-gear decisions on a certified, running motorcycle before any bespoke structure exists. Cheap, reversible, and it converts `chassis.md`'s paper geometry into measured data.*

**Scope**

- Front end + **wheels and tires** per `chassis.md`: Kineo true-tubeless pair, Pirelli Scorpion Rally STR **120/70-17 (58H)** front / **170/60-17 (72V)** rear, Brembo brake hardware as applicable to the stock fork/caliper interface.
- **Original Yamaha triple clamps retained**, with the **lower clamp machined an extra 1 mm**. ⚠ Safety-critical machining — document before cutting: exactly what interface the +1 mm accommodates, the finished bore, remaining wall thickness, and re-validated clamp-bolt torque. One-way modification on the only clamp set the bike has — measure twice. *(Consistent with the `chassis.md` "no machining of the fork" rule — the clamp is the sacrificial part, never the fork.)*
- Rear: 170/60-17 STR on the **stock GP swingarm** — confirm tire-to-arm and tire-to-chain clearance at the 170 section (the `chassis.md` tire-note check, brought forward).

**⚠ Kineo fitment fork — decide at order.** The spec'd Kineo rear (17×4.5, 8-pin cush + Ergal carrier) is built for the **bespoke swingarm**; Step 1 needs **XSR900-fitment** hubs. A wheel built for one won't carry to the other without re-hubbing. Either order GP-fit wheels for Step 1 and bespoke-fit later (two orders — budget it), or confirm with Kineo what's convertible. **Tone-ring provision on both orders regardless** (ABS gate, `chassis.md` §1). ~18-week lead applies.

**Gate:** geometry, stability and handling validated on the actual STR tires with real measurements (trail, sag, clearances) → these become the frame-design inputs for Step 2, replacing paper targets.

## Step 2 · Custom frame and triple clamps

*The bespoke structure, designed to Step-1 measured data rather than estimates.*

- Featherbed frame + swingarm + rising-rate linkage (`chassis.md` §1), frame jig first (`build.md` §4.2).
- **Bespoke yokes + billet-steel stem** (`chassis.md` §2) — stem dims from the measured GP stem (mule Phase 0/3b) + Yamaha microfiche; the Öhlins FG 621 enters here with its 43 mm tubes in the bespoke clamps.
- Rolling mock-up → clearances, radiator packaging → freeze geometry → **only then** order the built-to-order STX 46 shock.
- Kineo wheels in final (bespoke-arm) fitment if Step 1 ran GP-fit hubs.

**Gate:** rolling chassis on frozen geometry; steering-stem load check passed; `build.md` §4 phases 2–3 complete.

## Step 3 · Refine product for sale

*From one good bike to a certifiable, repeatable product.*

- DfM pass on the top cost/labour drivers (frame, exhaust, harness) — jig-repeatable fabrication, tracked per-unit hours.
- Donor pipeline industrialized (intake → jigged teardown → part-out — `analysis.md` §4).
- Homologation program engaged (Technical Service, type-approval per `emissions_certification.md` rollout), CoP procedures, technical file, RbW safety case.
- Economics re-baselined from measured build hours + real quotes (`economics.md`).

**Gate:** first type-approved, production-intent unit built to documented process.

---

## Caveats

1. **The GP is carrying two programs** — this vehicle roadmap and the ECU mule program share one motorcycle. Front-end work (mechanical, reversible) and ECU bench work can interleave, but don't stack an unproven custom ECU *and* an unproven front end for the same test ride — change one thing at a time.
2. **Step 1 machining is the only irreversible act on the GP** — everything else about Step 1 must stay revertible to stock.
3. **Long leads don't wait for steps** — Kineo (~18 wk) and the shock (built-to-order, gated on frozen geometry) are ordered on the `build.md` §3 calendar, not when a step "starts."
