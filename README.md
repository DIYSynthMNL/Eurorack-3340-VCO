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

What's available for builders, and what's still on the TODO list:

- [x] Schematic PDF (latest Rev 0.1.2) — [3340-VCO-Schematic-Rev0.1.2.pdf](schematic%20pdfs/3340-VCO-Schematic-Rev0.1.2.pdf)
- [x] KiCad source files — [kicad/](kicad/)
- [ ] Gerber files for PCB fabrication — *not yet exported — generate from kicad/ before sending to a fab*
- [x] Bill of materials (BOM) — [BOMs - 3340 VCO - Schematic Rev 0.1.0.pdf](BOMs/BOMs%20-%203340%20VCO%20-%20Schematic%20Rev%200.1.0.pdf)
- [x] 3D-printed front panel STL — [3340_VCO.stl](3D%20printed%20front%20panel/3340_VCO.stl)
- [ ] Front panel graphics (SVG/PDF for fab-made panels) — *not yet exported*
- [ ] Photos of the assembled module — *not yet — coming soon*
- [ ] Demo video — *not yet recorded*
- [ ] Build / assembly instructions — *not yet written*
- [ ] Calibration / tuning notes — *not yet written*
- [ ] License — *no LICENSE file yet*

If you want to help fill a gap (build photos, gerbers, an assembly guide), open an issue or PR.
