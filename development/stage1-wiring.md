# Stage-1 Wiring — microRusEFI data logger on the CP3 mule

Bench wiring for the **characterization data logger** (mule runbook Phase 1):
the MRE observes the engine — it drives **nothing**. Do not wire injectors,
coils, the ETB, or any TLE8888 output at this stage; those looms stay off the
bench until the RbW safety gate work begins.

Sources: MRE connector IDs from [`src/pins.rs`](https://github.com/sigmatactical-org/sigma-racer-efi/blob/main/src/pins.rs) /
[`src/analog.rs`](https://github.com/sigmatactical-org/sigma-racer-efi/blob/main/src/analog.rs) (rusEFI `board_configuration.cpp` naming)
and the [rusEFI MRE wiring guide](https://wiki.rusefi.com/Hardware-microRusEfi-wiring).
Authoritative per-pin view: [rusefi.com/docs/pinouts/microrusefi](https://rusefi.com/docs/pinouts/microrusefi/).

---

## Session 0 first: side-by-side against the OEM ECU

Before any characterization is trusted, run the bike **stock** and compare
the MRE's readings against the OEM ECU's own reporting — the factory
calibration is the reference instrument, and this session is read-only
(warranty intact, OEM loom untouched):

1. **CAN/OBD logging:** USB-CAN adapter on the diagnostic connector
   (`sigma-instrumentation` SocketCAN + `dbc-rs` decode); log OEM-reported
   CLT, IAT, TPS, RPM, battery V. Protocol known (desk-checked,
   `donor-desk-checks.md`): 6-pin RED connector, **ISO 15765-4 CAN,
   11-bit, 500 kbaud** — use the 6-pin→OBD2 adapter cable; first
   10 minutes on the bike confirm which standard PIDs it serves. Same
   session as the immobiliser sniff (runbook Phase 1, item 10).
2. **MRE voltage taps (Mode B rules below):** battery sense, plus the CLT
   node and TPS signal into **AV inputs** (voltage-only).
3. **Warmup cycle** cold → hot: OEM °C vs tapped volts **derives the CLT
   transfer function empirically** — settles the 3.3 V-vs-5 V NTC
   divider-top question with data, and covers runbook Phase 1 item 8
   without pulling a sensor. A grip sweep does the same for TPS/APP.
4. Time-align both logs (the DL→MDF4 converter's job); disagreement beyond
   tolerance = fix the firmware constant before proceeding.

Only after Session 0 agrees does Mode A (invasive, MRE-owns-sensors)
characterization begin.

## Choose the mode before touching the harness

**Mode A — MRE owns the sensors (primary).** OEM ECU disconnected, engine
spun on the starter with plugs out, or engine off for static sensor sweeps.
All rows in the signal table apply. This is the Phase-1 trigger-capture mode.

**Mode B — passive tap while the OEM ECU runs the engine.** Only for
observing a *running* engine. Restrictions:

- **Never tap CLT/IAT into the MRE's AT inputs while the OEM ECU is
  connected.** The AT inputs carry an onboard 2.7 kΩ pull-up (to 5 V); the
  OEM ECU has its own bias. Paralleling them corrupts **both** readings and
  can set OEM fault codes. Tap biased sensors into spare **AV inputs**
  (voltage-only, 500 kΩ pull-down) instead.
- **VR crank tap is a signal-integrity risk** — the MRE's VR conditioner
  input loads the sensor the OEM ECU is also using. Scope the OEM-side
  signal with and without the tap before trusting it; prefer Mode A for
  trigger characterization.
- TPS/APP taps (ECU-powered, low-impedance outputs) into AV inputs are fine.

## Bench BOM

- MRE board + its 48-pin connector kit or pigtail
- SWD probe (ST-Link class) for `probe-rs` + defmt/RTT
- Fused 12 V supply: bench PSU or battery, **5 A inline fuse**, switched
- Twisted-pair wire for crank/cam runs; multimeter; oscilloscope for VR checks

## Power (wire first, verify before energizing)

| Function | MRE main-connector pin | Wire to | Notes |
|---|---|---|---|
| +12 V supply | ⚠ confirm on the [interactive pinout](https://rusefi.com/docs/pinouts/microrusefi/) before power-up | Fused, switched 12 V | 9–22 V operating; 5 A fuse |
| Power ground `pgnd` | **#2, #6** | Engine block / chassis star point | Solid, short |
| Signal ground `sgnd` | **#17, #21** | Sensor grounds only | **Do not ground to engine** (rusEFI rule — keeps sensor returns clean) |
| 5 V sensor supply | ⚠ confirm pin | Sensors the MRE owns (Mode A) | 200 mA max per pin; unused in Mode B |

Continuity-check pgnd↔supply return and sgnd isolation from block *before*
first power. First power-up with nothing but power wired: both status LEDs
should behave per the README (running slow-blink, comms heartbeat).

## Signals (stage-1 firmware map)

| Signal | MRE pin | MCU pin / channel | Firmware field | Mode |
|---|---|---|---|---|
| Crank trigger (VR cond.) | **45** | PC6 / EXTI6 | `DL,T,C` records | A (B with scope check) |
| Cam trigger (hall) | **25** | PA5 / EXTI5 | `DL,T,V` records | A (B usually OK) |
| Battery sense | **1** | PC1 / ADC11 | `vbatt_v` | A + B |
| CLT (AN temp 1) | **18** | PA0 / ADC0 | `clt_c` | **A only** (onboard pull-up) |
| IAT (AN temp 2) | **23** | PA1 / ADC1 | `iat_c` | **A only** (onboard pull-up) |
| TPS / MAP (shared, MRE default) | **28** | PA4 / ADC4 | `tps_map_v` | A + B |
| AN volt 1 (spare / tap) | **27** | PC0 / ADC10 | `an_volt1_v` | A + B |
| AN volt 2 (spare / tap) | **26** | PA6 / ADC6 | `an_volt2_v` | A + B |

Wiring practice: crank/cam in twisted pair, routed away from any future
coil/injector looms; sensor returns to **sgnd**, never the block; strain
relief at the connector (the loom standards in `electrical.md` apply to the
bike, but the bench loom should not embarrass them).

### VR vs Hall on the crank input

Pin 45 feeds the board's VR conditioner — and the board is ordered as a
**VR or Hall variant**, so the variant must match the sensor. The CP3's
crank sensor type is **unverified** (runbook Phase 1, item 6): scope it at
the sensor connector while cranking before wiring it to the MRE. Expect VR
(reluctor + 2-wire sensor); if it turns out Hall (3-wire), the Hall-variant
input and 5 V supply apply instead. Polarity matters for VR — capture both
orientations if the gap signature looks wrong.

## Verify before trusting a single record

1. **Battery sense:** compare `vbatt_v` against a multimeter at the battery.
   Expect agreement within ~0.1 V (scaling constant `VBATT_DIVIDER`).
2. **CLT/IAT sanity (Mode A):** with a known 2.5 kΩ resistor across the CLT
   input, `clt_c` should read ≈25 °C. The NTC model is parametrized in
   firmware (`NtcConfig`: `bias_supply_volts` default **5 V** per the rusEFI
   wiring doc, `input_divider` default 1.0 — both ⚠ [MEASURE]); **this
   resistor check + the Session-0 warmup fit settle both constants
   empirically** before real temperatures are logged.
3. **TPS/AV channels:** feed 0 V and a known mid-scale voltage; confirm
   `tps_map_v` tracks (the 1.68 divider is applied in firmware).
4. **Trigger:** spin the engine on the starter, plugs out (runbook Phase 1,
   item 6). `DL,T,C` gap-ratio should sit near 100 tooth-to-tooth with a
   repeating spike (≈200 for one missing tooth, ≈300 for two) once per
   revolution. Same tooth count between consecutive spikes = the wheel.

## Capture

```bash
cargo build --release --features firmware,engine-yamaha-cp3 --target thumbv7em-none-eabihf
probe-rs run --chip STM32F767VI \
  target/thumbv7em-none-eabihf/release/sigma-racer-efi | tee capture-$(date +%Y%m%d-%H%M%S).log
```

Record formats (`DL,S` sensors at 10 Hz, `DL,T` per trigger edge,
`DL,X` drop warnings) are documented in the [README](https://github.com/sigmatactical-org/sigma-racer-efi/blob/main/README.md). Keep
every capture file — these are the Phase-1 characterization sheet's raw data.

## Explicitly out of scope at stage 1

Injector outputs (37/38/41/42), ignition outputs (9–12), GP outputs
(33/34/35/43), low-sides (3/7), ETB — **nothing on the output side gets
wired** until the bench progresses past the runbook's Phase 4/5 gates.
