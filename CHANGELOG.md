# Changelog

Development progress of the (private) Webcam VNG codebase. High-level summary only.

## September 2026 — preparing for the validation study

- **Standardised protocol "VNG-40cm" 1.0**: stimulus defaults tuned for a 40 cm viewing
  distance (saccades ±17° horizontal / ±10° vertical with randomised order and timing;
  smooth pursuit 0.3 Hz, ~31 °/s; OKN 20 °/s). Manual override kept; deviations are recorded.
- **Positioning step before every test**: live viewing distance from iris size; the test
  starts only inside the protocol zone. Distance drift during the recording is flagged.
- **Recording provenance**: code version, analysis-method version, camera, protocol and the
  exact stimulus shown are stored with every recording.
- **Saccade accuracy** (primary saccade gain) computed from the per-visit calibration.
- **Calibration grid** now spans the full stimulus range (no extrapolation at the edges).
- **Tracking quality control**: tracking loss is no longer mistaken for blinks; unusable
  recordings are flagged before saving.
- Fixes: physically impossible angles are discarded instead of clipped; OKN stimulus
  direction; vertical OKN analysed on the vertical channel; honest reporting of metrics
  that 30 fps cannot resolve.
- Repository hygiene: legacy UI and dead code removed; test suite of 16 regression suites.

## August 2026

- Smooth-pursuit velocity chart: eye vs. target velocity, drawn from exactly the samples
  used for the gain.

## July 2026 — from script to clinical workflow

- Migration to Python 3.11 and Qt 6 (PySide6) with a bit-identical numerical regression.
- Data layer: patient → visit → examination records in SQLite; archive view; hierarchical
  on-disk storage with safe deletion.
- Per-visit 9-point calibration with a shared scale for both eyes and an angular-range check.
- Chart dispatcher per test and pattern; clinical metrics table with versioned norms;
  XY trajectory for 2-D pursuit patterns; per-visit PDF report.
- Measured frame rate and stimulus geometry captured with every recording.
- Adaptive, frame-aspect-independent blink detection.
- Single I-VDT event detector with an adaptive velocity threshold replaces earlier
  pixel-based analyses; angular (degree-based) analysis throughout.

## 2025 — first prototype

- Webcam iris tracking, stimulus generation (saccades, smooth pursuit, OKN), pixel-based
  analysis and PDF/Excel export.
