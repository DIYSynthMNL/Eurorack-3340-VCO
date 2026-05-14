# Eurorack-3340-VCO

A Eurorack VCO module based on the [AS3340](https://electricdruid.net/product/as3340-vco/) chip from Electric Druid — a drop-in clone of the classic Curtis CEM3340. Analog 1V/oct tracking with simultaneous saw, triangle, sine, and pulse outputs.

## Features

- **1V/oct tracking** with two summed V/oct CV inputs (use both for transpose/unison)
- **Course tune** with jumper-selectable range (narrow / wide via JP1) plus **Fine tune** pot
- **Linear FM input** with attenuator pot (Lin FM, ±5V CV)
- **PWM input** with amount attenuator (±5V CV), feeds the chip's pulse-width modulator
- **Hard / Soft Sync** input with panel switch for selection (AC-coupled, 1 nF)
- **Four simultaneous outputs (10 Vpp)**: Saw, Triangle, Sine (diode-shaped from triangle), Pulse
- **Three calibration trims**:
  - Scale trim (RV1) — V/oct gain
  - High-Frequency Tracking trim (RV7) — accuracy at high notes
  - Sine amplitude trim (RV6) — tri-to-sine shape
- **Polystyrene timing capacitor** (C8, 1 nF) for low temperature drift
- Eurorack ±12V power via either 16-pin IDC or 3-pin JST connector

## Inputs and outputs

| Jack | Range | Notes |
|---|---|---|
| V/oct 1 | ±5V | Summed with V/oct 2 at the frequency-control node |
| V/oct 2 | ±5V | Summed with V/oct 1; direct (no attenuator) |
| Lin FM | ±5V | Through RV2 attenuator pot, AC-coupled into chip's Linear FM input |
| PWM | ±5V | Through RV3 amount pot, scaled to ~0–5V into chip's PWM-In |
| Sync | gate/audio | AC-coupled (1 nF), SW1 routes to Hard Sync (down) or Soft Sync (up) |
| Saw Out | 10 Vpp | Buffered, 1K series, ±5V swing |
| Tri Out | 10 Vpp | Buffered, 1K series, ±5V swing |
| Sine Out | 10 Vpp | Diode tri-to-sine shaper, amplitude trim, buffered |
| Pulse Out | 10 Vpp | Buffered, 1K series, ±5V swing |

## Block diagram

```
   V/oct 1 ─┐
   V/oct 2 ─┼──[summing node, 10K + 10K + 47K (course) + 1M5 (fine)]─► AS3340 Freq Control
   Course  ─┤                                                        ├─► Saw    ─► [×2.09 buffer] ─► Saw Out
   Fine ────┘                                                        ├─► Tri    ─► [×2.09 buffer] ─► Tri Out
                                                                     │                          └► [diode shaper + RV6 amp trim] ─► Sine Out
   Lin FM ─► [×RV2 amount] ─► [bias network: 1M5/+12V, 470R/GND] ──► AS3340 Lin FM In           
                                                                     │
   PWM CV ─► [×RV3 amount + 100K/200K/100K conditioner] ───────────► AS3340 PWM In ◄─── [10K hysteresis from Pulse Out]
                                                                     │
   Sync in ─► [1 nF AC-couple] ─► SW1 ─► Hard Sync / Soft Sync ────► AS3340 Sync
                                                                     │
                                                                     └─► Pulse  ─► [×2.09 buffer] ─► Pulse Out

   Calibration trims:
     RV1 (Scale)  → AS3340 Scale1/Scale2 pins (V/oct gain)
     RV7 (HFT)    → AS3340 HFT pin (high-frequency correction)
     RV6 (Sine Amp) → tri-to-sine output buffer (sine amplitude)

   Eurorack ±12V ─► U3 (78M05) / U4 (79M05) ─► ±5V rails (op-amp + chip VEE)
   Timing cap: C8 = 1 nF polystyrene (critical: do not substitute ceramic)
```

## Power

- Eurorack ±12V via **J10** (3-pin JST) or **J11** (16-pin IDC) — populate one
- Local U3 (78M05) makes +5V from +12V
- Local U4 (79M05) makes −5V from −12V; this becomes the AS3340's VEE pin voltage
- R39 / R40 (10K) are optional minimum-load resistors
- D3 / D4 — reverse-polarity protection diodes
- **AS3340 VEE protection:** Because VEE is driven from −5V (not −12V directly), no current-limiting resistor is needed on the chip's VEE pin. If you ever want to drive VEE from −12V directly, you'd need an 470Ω current limit resistor (see datasheet § Absolute Max).

## Calibration

The board has three trim pots that interact. Adjust in this order. You'll need: a multimeter, a frequency counter or tuner (a phone tuner app works), and a stable temperature environment (let the module warm up ~10 minutes first — the chip drifts thermally during warm-up).

**Step 1 — Scale trim (RV1).** Sets the V/oct gain. This is the most important trim for musical accuracy.

1. With no CV patched and Course/Fine at 12 o'clock, note the output frequency.
2. Patch a known reference voltage into V/oct 1 (e.g., 0V from a calibrated source or shorted to GND). Tune Course/Fine until the saw output matches a reference note — say C2 (65.41 Hz).
3. Apply +1V to V/oct 1. The output should rise exactly one octave (C3 = 130.81 Hz). If it's high, lower RV1 slightly; if low, raise it.
4. Step the input voltage up to +4V or +5V and verify the output is still tracking 1V/oct. Iterate RV1 + the tune knob until accurate across 5+ octaves.

**Step 2 — High-Frequency Tracking trim (RV7).** Compensates for internal comparator delay at very high notes.

1. With the V/oct calibrated (Step 1), apply +6V or +7V to push the output to ~8 kHz+.
2. Compare actual output frequency to expected (e.g., from 65.41 Hz baseline, +7 octaves = 8372 Hz).
3. Adjust RV7 to correct the deviation. RV7 mostly affects high frequencies — it should not noticeably shift low-frequency tuning.
4. Re-verify Step 1 calibration. If low-frequency tracking shifted, iterate.

**Step 3 — Sine Amplitude trim (RV6).** Sets the tri-to-sine shape and amplitude.

1. Patch a scope on the Sine Out jack with a steady tone (e.g., A4 = 440 Hz).
2. Adjust RV6 until the waveform looks like a clean sine — not too peaked (under-trimmed) and not flat-topped (over-trimmed).
3. By ear: clean smooth fundamental, no harsh harmonics.

## References

- [AS3340 datasheet](http://www.alfarzpp.lv/eng/sc/AS3340.pdf)
- [Electric Druid AS3340 product page](https://electricdruid.net/product/as3340-vco/)
- [Electric Druid CEM3340 VCO designs](https://electricdruid.net/cem3340-vco-voltage-controlled-oscillator-designs/)
- Design inspiration: [Kassutronics 3340 VCO](https://github.com/kassu/kassutronics/tree/master/documentation/VCO%203340), [YuSynth VCO](https://yusynth.net/Modular/EN/VCO/index.html)
- [Tri-to-sine shaping techniques (Tim Stinchcombe)](https://www.timstinchcombe.co.uk/index.php?pge=trisin)

## Build status

What's ready for builders today, and what's still on the TODO list:

**Production assets** (what you need to actually fabricate and assemble a final unit)

- [x] Schematic — Rev 0.1.2 ([PDF](Schematic%20PDFs/3340-VCO-Schematic-Rev0.1.2.pdf))
- [ ] PCB layout — in progress — single working layout in `kicad/`, not yet separated for fab. The current rev is labeled "Prototype."
- [ ] Gerber files for fabrication — none yet
- [x] BOM — [Rev 0.1.0 PDF](BOMs/BOMs%20-%203340%20VCO%20-%20Schematic%20Rev%200.1.0.pdf) *(critical: use polystyrene for C8 timing cap, not ceramic)*
- [ ] Final front panel (SVG/PDF for fab) — none yet
- [ ] License — none yet

**Prototype assets** (for breadboard / perfboard / 3D-printed-panel builds before final PCB)

- [x] 3D-printed prototype panel STL — [3340_VCO.stl](3D%20printed%20front%20panel/3340_VCO.stl)
- [x] Falstad simulations of sub-circuits — [falstad/](falstad/)

**Documentation**

- [ ] Photos of the assembled module — none yet (drop in [`photos/`](photos/))
- [ ] Demo video — none yet
- [ ] Build / assembly instructions — none yet
- [x] Calibration / tuning notes — see "Calibration" section above

Want to help fill a gap (build photos, gerbers, an assembly guide)? Open an issue or PR.
