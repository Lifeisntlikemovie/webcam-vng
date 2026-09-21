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
- **Camera calibration from a chessboard target**: the real focal length replaces a
  geometric approximation, so the viewing distance is measured rather than estimated.
  A printable board and a guided capture dialog are built in.
- **Settings tab**: camera selection (the built-in camera is now the reliable default
  instead of whichever device the OS enumerates first), screen size, calibration profile
  per camera and resolution.
- **Stimulus presentation reworked**: full-screen during countdown and recording; capture
  and tracking moved off the UI thread; the stimulus is drawn on its own 60 fps timer, and
  every camera frame is paired with the target position actually on screen at that instant.
  The stimulus refresh rate is measured and stored, so a stuttering presentation can no
  longer be mistaken for a weak patient response.
- **Analysis method 3.0**: several estimators revised and validated against synthetic
  recordings with known ground truth, with a bit-exact regression test to keep the numbers
  reproducible. Stored examinations can be recomputed with the current method.
- **One analysis path** shared by the preview, the visit report and the dataset export —
  a report can no longer contradict the chart printed below it.
- **Research dataset export** (XLSX/CSV): one row per examination, all computed with a
  single method version, patient code / age / sex only.
- **Reference-interval algorithm for norms**: CLSI-style limits with outlier removal,
  bootstrap confidence intervals and an age-dependency check. The subject, not the
  recording, is the unit. No norms are applied until explicitly approved.
- **Methodology and About tabs**: how each test is run and what every manual parameter
  changes, with the protocol values filled in from the live configuration.
- Fixes: physically impossible angles are discarded instead of clipped; OKN stimulus
  direction; vertical OKN analysed on the vertical channel; honest reporting of metrics
  that 30 fps cannot resolve.
- Repository hygiene: legacy UI and dead code removed; stricter rules on what may enter
  version control; test suite of 21 regression suites.

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
