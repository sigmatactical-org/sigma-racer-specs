# Sigma — Bodywork & Ergonomics

*Companion to `README.md`. The bodywork half of the café racer's character — **minimalist**: tank, seat/cowl, subframe, fenders, the rider triangle (clip-ons + rearsets) and the hand/foot controls. Chassis & running gear live in `chassis.md`; engine in `engine.md`; electrical/switchgear in `electrical.md`; the cockpit display in `electronics.md` §8. Flat-black finish and the sourcing rule come from the `README.md` hub.*

---

## 1 · Bodywork

**Design language — minimalist `[LOCKED]`.** Strip to the essential: the bodywork's job is to *get out of the way* and let the mechanicals be the aesthetic — the featherbed frame, the CP3 triple, and the Öhlins / Brembo / Kineo jewellery are the styling (they're the build's purpose, `README.md`). Principles:

- **Few parts, clean lines** — slim tank, solo seat, short tail, small round LED headlight.
- **Expose the mechanical, hide the ugly** — route the loom internally, tuck the cockpit compute + DC-DC out of sight, minimise visible fasteners and brackets.
- **Flat-black restraint** — no graphics, no chrome; interest comes from material + texture contrast, not decoration.
- **Integrate the tech invisibly** — the 6.86" bar cockpit (`electronics.md` §8) is the single modern touch, flush-mounted; everything else reads classic-minimal.
- Minimalism also serves the **≤190 kg target** (`build.md` §1) — less bodywork, less mass.

| Item | Spec | Status |
|---|---|---|
| Design language | **Minimalist** — expose the mechanicals, few clean parts, flat-black restraint, tech hidden (principles above) | `[LOCKED]` |
| Fuel tank | Bespoke **slim café teardrop**, hand-formed alloy; minimal — no graphics, flush/hidden filler; knee-cutaways to the narrow triple; capacity + vent + evap take-off to suit (`engine.md`) | `[BESPOKE]` |
| Seat / cowl | **Solo** café seat + minimal short tail cowl; thin flat-black upholstery; no pillion | `[BESPOKE]` |
| Subframe | Minimal **exposed tube** subframe to the featherbed rear (part of the look); carries seat + tucked LED tail + plate; sized to the shock/linkage top mount | `[BESPOKE]` |
| Front fender | *(Speced in `chassis.md` §2 — minimal blade off the FG 621 lowers)* | — |
| Rear / tail | Minimal **tail-tidy**: tucked LED tail/stop + plate hanger (road-legal placement — `emissions_certification.md`); no bulky rear fender | `[PENDING]` |
| Headlight | Small **round LED** headlight, minimal or no nacelle; clean mount to the yokes | `[PENDING]` |
| Material / finish | Alloy + carbon + minimal steel; **flat black throughout**, per-material texture for interest | `[PENDING]` |

## 2 · Rider triangle (ergonomics)

| Item | Spec | Status |
|---|---|---|
| Clip-ons | Premium adjustable clip-ons to the FG 621 43 mm tubes (or bespoke) — café reach, above/below top yoke TBD by the yoke design (`chassis.md` §2) | `[PENDING]` |
| Rearsets | Premium adjustable rearsets (billet) — shift/brake linkage to the CP3 gearbox + the rear master (`chassis.md`) | `[PENDING]` |
| Seat height / reach | Set by subframe + seat build; validate rider fit against the frozen chassis geometry | `[PENDING]` |
| Mirrors | Bar-end or stalk mirrors — must meet road-legal field-of-view for approval | `[PENDING]` |

## 3 · Controls & actuation

| Item | Spec | Status |
|---|---|---|
| Throttle | Ride-by-wire twistgrip — **dual APP sensors** read by the ECU (`electronics.md` §2/§6); no cable. Grip assembly must house/interface the APP unit | `[LOCKED]` (RbW) / `[PENDING]` grip |
| Clutch actuation | Retained CP3 assist/slipper clutch (`engine.md`) — **decide cable vs hydraulic** master + lever; hydraulic suits the clean café look, cable is simpler | `[PENDING]` |
| Front brake | Brembo 19 RCS radial master + lever *(speced in `chassis.md` §2)* | — |
| Levers / grips | Premium adjustable levers; grips to suit | `[PENDING]` |
| Switchgear | Bars switches (start/kill, lights, indicators, horn, mode) → the ECU / CAN — **speced in `electrical.md`** | — |

## 4 · Open items `[PENDING]`

- Whole domain is early: lock the **frozen chassis geometry** (`chassis.md`) and the **subframe/shock top-mount** before committing tank/seat/subframe shapes.
- Clutch actuation (cable vs hydraulic) gates the left-bar + lever choice.
- Confirm **road-legal** mirror field-of-view, plate/light placement and rider-visibility items for EU/UK **type-approval** (for sale — `emissions_certification.md`).

---

# Caveats (bodywork)

1. **Bodywork keys off frozen geometry** — tank, seat and subframe shapes can't finalize until the chassis geometry and shock/linkage top mount are locked; build the rider triangle to the validated chassis, not the other way round.
2. **Road-legal equipment is part of bodywork** — mirrors, plate/lighting placement and rider ergonomics feed the homologation checklist; treat them as approval items, not just styling.
