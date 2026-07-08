# Sigma — Design-for-Manufacture Pass (Gate 2)

*Dev note (2026-07-07). The analysis's finding 3 ("DfM becomes mandatory") turned into design constraints. Scope: the three per-unit labour drivers — frame, exhaust, harness. These are **inputs to Step 2's design work**, not suggestions: a frame designed without them gets redesigned. Targets assume ~10–50 units/yr under the small-series cap; per-unit hours are the metric (`economics.md` carries ~150–300 h total build labour — this pass attacks the biggest slices).*

---

## 1 · Frame (chromoly featherbed) — from craft to kit + jig

**The DfM rule: the jig owns the geometry; the tubes are a kit; every critical bore is machined after welding.**

Constraints Step 2's frame design must inherit:

1. **Two primary datums, machined post-weld:** the headstock bore and the swingarm-pivot bore. The frame is fixtured *from* these; everything else references them. Both get welded with machining stock (+1.5–2 mm) and are line-bored/faced **in one setup** after welding — weld distortion becomes a machining allowance, not a scrap cause. Bearing seats are never as-welded.
2. **Modular fixture, not a dedicated art-piece jig:** flat tooling table + headstock tower + pivot tower + engine-mount pucks on dowel-located risers. The engine's mounting points are jig features (dummy engine or mount plates drilled from a measured CP3) — the engine *is* the mid-frame reference, which also guarantees every frame accepts every engine.
3. **Tube kit from cut files:** every tube CNC mandrel-bent + laser/tube-notched from released DXF/STEP — no hand-fitted fish-mouths. Design rules to make that possible: bends in **max two planes per tube**, minimum straight between bends per the bender's spec, one tube OD/wall family per structural role (catalog chromoly sizes only), and joint designs that self-locate (saddle depth = positive stop).
4. **Documented weld sequence** (tack map → root sequence alternating sides → final), written once during frame #1–#3 and then frozen; distortion is repeatable if the sequence is.
5. **QC per frame, 15 min not an afternoon:** check sheet of ~8 measurements from the two datums (neck angle, pivot parallelism ≤0.1 mm/100 mm, pivot-to-neck distance, engine-mount trueness) with go/no-go tolerances; results filed in the CoP record per VIN.
6. **Subframe stays bolt-on** (already spec) and becomes the tolerance sponge: seat/tail fit adjusts at the subframe shims, never by bending the main frame.

**Hours target: ~60 h (one-off craft) → ≤24 h/frame** (kit prep 4, jig load+tack 4, weld 8, machine datums 4, QC+finish prep 4).

## 2 · Exhaust (ti 3-into-1, side exit) — section discipline

**The DfM rule: a fixed section count from a released cut library, welded in a dedicated tack fixture; the cat is a purchased module.**

1. **≤ 9 formed pieces total** for the full system: 3 primaries × 2 segments (CNC mandrel-bent ti, from the library — no pie-cut sculpture on production units; pie-cuts allowed only on the prototype to *find* the routing, then converted to bends), 1 merge collector (**purchased 3-into-1 ti collector**, catalog), 1 cat housing (**purchased metal-substrate cat module**, catalog, homologation paperwork attached), 1 muffler can + tip weldment.
2. **Header flange datum = the head.** Flange jig plate drilled from the measured CP3 head; primaries tack in a fixture that holds flange plate + collector + hanger points in the frame-jig coordinate system, so every system fits every frame without on-bike fitting.
3. **Slip joints at the two service planes** (collector→cat, cat→muffler) with springs/clamps — absorbs tolerance stack and makes the noise-compliance muffler swappable without cutting (drive-by limit engineering happens at the can, not the whole system).
4. **Purge-weld procedure documented** (ti back-purge rig is part of the fixture); weld count minimized by the section design, not by welder heroics.

**Hours target: ~25 h (one-off) → ≤10 h/system.**

## 3 · Harness (mil-spec loom) — board build, not bench art

**The DfM rule: the loom is manufactured on a full-scale board from a released drawing, and it isn't done until the tester says so.**

1. **Harness board** (full-scale, pegged, laminated print of the loom drawing) generated from the loom CAD — every branch length, breakout and clip point on the board. Nobody measures on the bike after unit #1.
2. **Released cut list**: every wire pre-cut/pre-labeled (M22759 gauge + circuit ID printed at both ends) as a kit before the board build starts. Kitting is unskilled time; board time is skilled time — split them.
3. **Crimp QC per mil practice**: calibrated M22520 tooling logged per session, pull-test coupons at shift start (sampling, not 100 %), heat-shrink labels not tape.
4. **Ring-out tester is a deliverable of the harness design**: a connector-pigtail test box (or bed-of-nails) that verifies every net + checks for shorts in minutes. A loom that hasn't passed the tester doesn't ship — this is also the CoP evidence.
5. **Design rules feeding this:** service loops standardized (one length), branch tolerances ±10 mm (the star topology absorbs it), connector count already minimized per `electrical.md` §0 — hold that line when the cockpit wants "one more sensor".

**Hours target: ~40 h (one-off) → ≤16 h/loom** (kitting 3, board build 9, terminate+test 4).

## 4 · The arithmetic (why this gate matters)

These three lines are ~125 h of the ~150–300 h estimate. This pass takes them from ~125 h → **~50 h/unit**: at shop rate that's roughly **$4.5–6k/unit off COGS** — comparable to the entire donor-vs-crate engine question, and it's entirely within our control. NRE cost: the tooling line already budgeted in `economics.md` (~$10–40k jigs/fixtures) covers the table, towers, exhaust fixture and harness boards.

## 5 · What Step 2 must deliver to satisfy this pass

- [ ] Frame CAD released **with** the fixture CAD (they are one design)
- [ ] Tube cut files + bend cards for every frame tube
- [ ] Post-weld machining drawing (datums, stock allowances, one-setup plan)
- [ ] Frame QC check sheet (8 measurements, tolerances, CoP filing format)
- [ ] Exhaust section library + flange/collector fixture design; cat + collector part numbers chosen from catalog
- [ ] Loom drawing → board print + cut list + tester netlist (generated, not hand-made)

*Review trigger: revisit hour targets after units #1–#3 with measured times (`economics.md` re-baseline).*
