# EMI Filter Design for an Offline Flyback SMPS

Simulation-based EMI filter design project, built in **SIMetrix/SIMPLIS**, covering the full workflow from noise source characterization through DM and CM conducted-emissions filtering, benchmarked against **CISPR 22 Class B**.

Built as a self-directed learning project to develop practical EMI filter design skills, ahead of applying for the EMV-Filter-Entwickler position.

## Project overview

- **Converter:** offline flyback SMPS, 5V / 2A output, universal-ish mains input (230Vac, 50Hz modeled)
- **Goal:** design a two-stage (DM + CM) conducted-emissions filter for a real, non-ideal switching noise source, and verify performance against CISPR 22B using a simulated LISN
- **Tools:** SIMetrix/SIMPLIS (schematic capture, transient simulation, FFT/spectrum analysis)

## Status

| Stage | Status | Summary |
|---|---|---|
| **Lesson 1 — Noise source & LISN** | ✅ Complete | Built and validated the flyback converter (bulk voltage, open-loop power balance, MOSFET stress, RCD snubber) and a two-line LISN. Captured the baseline conducted-emissions spectrum: 75-91 dBµV (150-500kHz), exceeding CISPR 22B by up to ~35dB. |
| **Lesson 2 — Differential-Mode (DM) filter** | ✅ Complete | Sized and simulated a single-stage DM LC filter (L_DM ≈ 15-16mH, Cx = 1µF). Diagnosed and fixed an unintended LC resonance with the bulk capacitor (added 5Ω damping resistors per line). Final result: all checked spot frequencies (150kHz/500kHz/5MHz) pass under the CISPR 22B limit by 8-42dB. |
| **Lesson 3 — Common-Mode (CM) filter** | 🔧 In progress | Added a parasitic drain-to-chassis capacitance to model real CM current paths, confirmed a ~40-50dB CM-driven excess in the 1-10MHz band, and are iterating on a CM choke (4.7-10mH, k≈0.995) + Y-capacitor (2.2nF, damped) design. Choke coupling behavior has been validated (differential-current suppression confirmed via a k=0 control test); currently isolating whether a remaining 300kHz-1MHz emissions hump is residual CM content or leftover DM content requiring a revisit of the Lesson 2 filter. |

## What's in this repo

- **`schematics/`** — SIMetrix `.sxsch` schematic files for each stage (noise source + LISN, DM filter, CM filter work-in-progress)
- **`docs/`** — Full written lesson notes: theory, hand calculations, simulation results, and the real debugging process (including root-caused issues and fixes, not just final "clean" numbers)
- **`images/`** — Key waveform and FFT spectrum captures referenced in the docs

## Highlights / what this demonstrates

- Full LISN + DM/CM filter simulation methodology, not just textbook formulas — actual worked hand calculations (e.g., snubber RCD sizing, DM corner-frequency targeting) validated and refined against SIMetrix simulation results
- Real debugging process included, not hidden: e.g., an LC resonance between the DM filter inductor and the bulk capacitor that was blocking real mains charging current, root-caused via elimination (ruled out unit errors, wiring mistakes) before identifying the actual resonance and fixing it with damping
- Quantified compliance gap analysis against CISPR 22 Class B at each stage, not just "it looks better"
- Ongoing, transparent CM filter debugging (Lesson 3), including a designed control experiment (k=0 coupling test) to isolate whether a choke is functioning as intended

## Next steps

- Resolve the remaining 300kHz-1MHz emissions hump (CM vs. residual DM)
- Finalize CM choke/Y-cap values and re-verify full-band compliance
- Document Lesson 3 with the same calculation + results format as Lessons 1-2

---
*Contact: [your name / email / LinkedIn] — happy to walk through the simulation live.*
