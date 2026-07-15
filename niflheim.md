---
title: Niflheim
description: Frequency-domain EM ground-conductivity processing.
---

<p align="center">
  <img src="assets/img/Niflheim_logo.png" alt="Niflheim logo" width="200">
</p>

# Niflheim — EM Ground Conductivity

**Niflheim turns a walked EM conductivity survey into clean, georeferenced
conductivity and inphase maps with anomalies flagged automatically.**

> Named for **Niflheim**, the primordial Norse realm of mist and ice — apt
> for a method whose response is dominated by pore water, salinity, and clay
> content. One of the EM31's most established applications is permafrost and
> frozen-ground mapping.

## What it does for you

- Reads Geonics **EM31-MK2** survey files directly and geolocates every
  sample from the instrument's embedded GPS stream.
- Handles **both channels** throughout: apparent conductivity (mS/m) and
  inphase (a magnetic-susceptibility proxy, ppt) are processed, gridded, and
  displayed side by side.
- Cleans field data with drift correction, despiking, detrending, and
  station binning.
- Grids both channels onto a map and flags conductivity and inphase
  anomalies automatically.

## Workflow

1. **Open your survey** — samples and the GPS track load in one step and
   plot on the map immediately.
2. **Calibrate** — apply survey-specific calibration factors when your
   instrument's raw counts need adjusting; settings persist with the survey.
3. **Process** — drift correction, despike, detrend, and station binning,
   each a labelled control.
4. **Grid and detect** — choose the interpolation (inverse-distance, linear,
   or nearest) and grid density (auto, dense, coarse, or custom); anomalies
   are flagged by statistical threshold and exported to CSV.
5. **View and export** — conductivity and inphase maps with adjustable value
   ranges, percentile clipping, and colormaps, plus profile views.

## Supported data

- **Geonics EM31-MK2** files with embedded GPS — read directly, no
  conversion step.

## Outputs & figures

- Gridded conductivity and inphase maps, ready for a report.
- GPS track and profile plots.
- Anomaly lists with map coordinates, exported to CSV.

## Part of the Yggdrasil platform

Niflheim runs standalone or inside the [Yggdrasil
application](https://yetiskier.github.io/yggdrasil-docs/yggdrasil.html), with a built-in Help menu that includes a
quad-vs-inphase primer. One click publishes conductivity and inphase maps,
GPS tracks, and detected anomalies into the project's shared 3D scene. EM
surfaces drape at a physically honest **effective depth** below ground
(about 1.5 m for EM31-class penetration), so a conductivity map sits beneath
a [Midgard](https://yetiskier.github.io/yggdrasil-docs/midgard.html) radar profile where the sensor actually senses —
joint interpretation without manual placement.

## Availability

Niflheim is commercially licensed as part of the Yggdrasil suite (Windows
and Linux). Contact **[joel@aesirmt.com](mailto:joel@aesirmt.com)** for
licensing and installers.

[← Back to the suite overview](https://yetiskier.github.io/yggdrasil-docs/yggdrasil.html)
