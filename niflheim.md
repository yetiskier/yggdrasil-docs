---
title: Niflheim
description: Frequency-domain EM ground-conductivity processing.
---

<p align="center">
  <img src="assets/img/Niflheim_logo.png" alt="Niflheim logo" width="200">
</p>

# Niflheim — EM Ground Conductivity

**Frequency-domain electromagnetic ground-conductivity processing for
shallow-earth surveys.**

> Named for **Niflheim**, the primordial Norse realm of mist and ice — apt
> for a method whose response is dominated by pore water, salinity, and clay
> content. One of the EM31's most established applications is permafrost and
> frozen-ground mapping.

Niflheim reads Geonics **EM31-MK2** ASCII (`.R31`) dumps, geolocates each
sample from the embedded NMEA GPS stream, applies a configurable processing
pipeline, grids both channels onto a map, and detects conductivity and
inphase anomalies — from a CLI, a desktop GUI, or as a panel in the
Yggdrasil shell.

## Capabilities

- **Two-channel handling throughout** — Quad (apparent conductivity, mS/m)
  and Inphase (magnetic-susceptibility proxy, ppt) are read, processed,
  gridded, and published side by side.
- **Geolocation** — the embedded NMEA stream becomes a per-sample lat/lon
  track, projected to UTM with a self-contained transform.
- **Calibration overrides** — survey-specific raw-counts → mS/m and → ppt
  scale factors, recorded in the survey header and round-tripped through the
  survey YAML.
- **Processing** — drift correction, despiking, detrending, and station
  binning ahead of gridding.
- **Gridding** — IDW / linear / nearest interpolation onto a regular map
  grid, with size presets (auto / dense / coarse / custom cell size and
  padding) selectable from the CLI config or the GUI.
- **Anomaly detection** — conductivity/inphase outliers flagged by z-score
  threshold and written to CSV.
- **Display controls** — value ranges, percentile clipping, colormaps, and
  profile scaling, all mirrored between the GUI and the survey YAML.

## GUI

The GUI exposes three persistent config groups — Display scales, Calibration,
and Grid scale — that round-trip through the survey YAML, plus a built-in
Help menu covering each section and a Quad-vs-Inphase primer.

## In the Yggdrasil shell

One command publishes conductivity and inphase maps, GPS tracks, and
detected anomalies into a Yggdrasil project's shared 3D scene. EM surfaces
drape at a physically honest **effective depth** below ground (default 1.5 m
for EM31-class penetration), so a conductivity grid sits under a
[Midgard](midgard.html) radar curtain where the sensor actually senses —
joint interpretation without manual placement. Any project containing EM
data surfaces the Niflheim panel automatically.

## Availability

Niflheim is commercially licensed as part of the Yggdrasil suite (Windows
and Linux). Contact **[joel@aesirmt.com](mailto:joel@aesirmt.com)** for
licensing and installers.

[← Back to the suite overview](yggdrasil.html)
