# Eurorack-3340-VCO

A Eurorack VCO module based on the AS3340 chip (Electric Druid). A V/oct analog oscillator with the classic CEM3340-family character.

## Schematic and BOM

- Latest schematic: **Rev 0.1.2** — [PDF](Schematic%20PDFs/3340-VCO-Schematic-Rev0.1.2.pdf)
- All revisions: [Schematic PDFs/](Schematic%20PDFs/)
- BOM: [Rev 0.1.0 PDF](BOMs/)

## Hardware

- Multiboard KiCad project (control board + main board): [kicad/](kicad/)
- 3D-printed front panel STL: [3D printed front panel/](3D%20printed%20front%20panel/)
- Falstad simulations: [falstad/](falstad/)

## Power

- Powered from Eurorack ±12V. The AS3340's VEE pin needs a current-limiting resistor when powered from −12V (≈470 Ω). See the AS3340 datasheet section in `Eurorack-3340-VCO/kicad/3340-VCO.kicad_sch` for the protection network.

## References

- [AS3340 datasheet](http://www.alfarzpp.lv/eng/sc/AS3340.pdf)
- [Electric Druid AS3340 product page](https://electricdruid.net/product/as3340-vco/)
- Design inspiration: [Kassutronics 3340 VCO](https://github.com/kassu/kassutronics/tree/master/documentation/VCO%203340), [Electric Druid's CEM3340 VCO designs](https://electricdruid.net/cem3340-vco-voltage-controlled-oscillator-designs/), [YuSynth VCO](https://yusynth.net/Modular/EN/VCO/index.html)
- [Tri-to-sin using a JFET (Tim Stinchcombe)](https://www.timstinchcombe.co.uk/index.php?pge=trisin)

## Build status

What's ready for builders today, and what's still on the TODO list:

**Production assets** (what you need to actually fabricate and assemble a final unit)

- [x] Schematic — Rev 0.1.2 ([3340-VCO-Schematic-Rev0.1.2.pdf](Schematic%20PDFs/3340-VCO-Schematic-Rev0.1.2.pdf))
- [ ] PCB layout — in progress — single working layout in `kicad/`, not yet separated for fab
- [ ] Gerber files for fabrication — none yet
- [x] BOM — [BOMs - 3340 VCO - Schematic Rev 0.1.0.pdf](BOMs/BOMs%20-%203340%20VCO%20-%20Schematic%20Rev%200.1.0.pdf)
- [ ] Final front panel (SVG/PDF for fab) — none yet
- [ ] License — none yet

**Prototype assets** (for breadboard / perfboard / 3D-printed-panel builds before final PCB)

- [x] 3D-printed prototype panel STL — [3340_VCO.stl](3D%20printed%20front%20panel/3340_VCO.stl)

**Documentation**

- [ ] Photos of the assembled module — none yet (drop in [`photos/`](photos/))
- [ ] Demo video — none yet
- [ ] Build / assembly instructions — none yet
- [ ] Calibration / tuning notes — none yet

Want to help fill a gap (build photos, gerbers, an assembly guide)? Open an issue or PR.
