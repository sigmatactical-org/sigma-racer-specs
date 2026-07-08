# Sigma — Donor Desk Checks (A2 fiche · GP diagnostics)

*Dev note (2026-07-07). Two open questions closed from the desk.*

## 1 · A2 (35 kW) MT-09 — hardware-identical, confirmed ✔

**Finding:** the A2 MT-09 is the standard bike with a different ECU calibration and paperwork. Evidence:

- Yamaha's own A2 implementation is a two-state ECU (35 kW bridé / 70 kW "full", the 95 ch homologation that satisfies the EU double-power rule) — the launch coverage stated the only technical change is the ECU (moto-net, 2022).
- French owner forums differentiate 95 ch vs 119 ch bikes **by the chassis plate/registration only** — "otherwise identical" (mt09.net).
- Aftermarket tuners (MC-R, NRBike) sell **ECU-reflash derestriction of A2 bikes to the full 119 ch including ride-mode unlock** — impossible unless the engine hardware is the full-power hardware.

**Consequence for the donor pipeline:** the A2 variant is a fully valid donor — our ECU discards Yamaha's map entirely, so the paper rating is irrelevant. **Buy on price: A2 or standard, whichever discounts harder** (A2 listed ~€300 under standard in FR). Belt-and-braces: at first donor teardown, spot-check cam/throttle-body part numbers against a standard fiche — 10 minutes, closes the question with metal.

## 2 · XSR900 GP diagnostics — protocol known, adapter ordered ✔

**Finding:** the gen-3 platform (2021+ MT-09/XSR900, hence the GP) speaks:

- **Connector:** 6-pin **RED** diagnostic connector (2016–2020 bikes used the 4-pin — buy the right cable).
- **Protocol:** **ISO 15765-4 CAN, 11-bit IDs, 500 kbaud** — standard OBD transport; generic scanners read fault codes on this platform, so standard PID polling is expected to work alongside Yamaha-proprietary frames.

**Session-0 shopping list (order with the USB-CAN adapter):**

- Yamaha **6-pin RED → OBD2 female** adapter cable (~€15, many vendors)
- The CANable/candleLight then connects either through that cable's CAN pins or an OBD2 breakout — `candump` at **500 k** from minute one
- Optional: any ELM327-class reader as a sanity cross-check of PID availability

**What remains on-bike (Session 0, first 10 minutes):** confirm which standard PIDs the GP actually serves (RPM/CLT/TPS expected) vs what needs sniffing from broadcast/UDS frames — the side-by-side plan in `stage1-wiring.md` works either way, candump captures everything.
