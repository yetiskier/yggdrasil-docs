---
title: Midgard
description: Near-surface common-offset GPR processing.
---

<p align="center">
  <img src="assets/img/Midgard_logo.png" alt="Midgard logo" width="200">
</p>

# Midgard — Surface GPR

**Midgard takes common-offset GPR lines from the instrument to migrated,
depth-true radargrams, target maps, and 3D fence diagrams.**

> Named for **Midgard**, the Norse middle realm of humankind — the shallow,
> lived-in ground where near-surface GPR looks for anthropogenic features:
> utilities, graves, foundations, voids, UXO.

## What it does for you

- Reads the major GPR manufacturers' files directly and geolocates every
  trace from the GPS track.
- Cleans and enhances the data with a full, reorderable processing
  pipeline.
- Determines velocity from hyperbola fitting, migrates, and automatically
  flags compact targets with depths and map coordinates.
- Visualizes in 2D (radargrams, survey maps, depth slices) and 3D (fence
  diagrams draped on the site terrain).

## Workflow

1. **Open your lines** — formats are detected automatically; the GPS track
   is interpolated to every trace and each line is resampled to true
   along-line distance, so hyperbolas plot and fit correctly. Lines without
   GPS fall back to even or odometer spacing.
2. **Process** — a drag-to-reorder pipeline: time-zero correction (five
   methods, including per-trace first-break alignment), dead-trace removal,
   spreading-loss gain, dewow, mean-trace removal, bandpass auto-tuned from
   the antenna frequency, eigenimage filtering, and clipping. Every
   parameter is a labelled control.
3. **Pick velocity** — click a hyperbola apex and drag the limbs to fit; a
   semblance scan provides the initial guess. Each pick carries a depth and
   map coordinates, overlays on the radargram, and exports to CSV.
4. **Migrate and detect** — Kirchhoff or Stolt migration collapses
   point-target hyperbolas; automatic detection then suppresses laterally
   continuous geology so compact anomalies pop, reporting each target with
   along-line position, depth, strength, and map coordinates.
5. **View in 2D and 3D** — radargrams, depth slices, fence diagrams, and
   the shared project scene.

![Plan-view GPS survey map coloured by line and elevation](assets/img/map_both.png)

![Processed radargram](assets/img/radargram_final.png)

*Radargrams support time or depth axes in metres, feet, and nanoseconds (any
combination on one figure), true-scale aspect, and topographic correction.*

## Supported data

- **MALA / RAMAC** (with GPS track files)
- **Sensors & Software**
- **GSSI** `.DZT`

## Outputs & figures

- **Radargrams** — processed or migrated, time or depth axes, topographic
  correction, publication-ready.
- **Target reports** — automatic detections as a labelled overlay and a CSV
  of positions, depths, and strengths.

![Automatic target detection on a migrated section](assets/img/malags_targets.png)

- **Depth slices (C-scans)** — every trace at its true map position,
  coloured by amplitude at depth, on one global colour scale so slices at
  different depths stay comparable. A slider sweeps depth live.
- **3D fence diagrams** — radargram curtains standing at their true GPS
  paths with depth slices floated in the same view, plus contact sheets and
  an orbiting-turntable animation export.
- **3D data cube** — many lines combined onto a regular grid for export and
  interoperability.

![3D fence diagram of a serpentine survey](assets/img/fence.png)

## Part of the Yggdrasil platform

Midgard runs standalone or inside the [Yggdrasil
application](yggdrasil.html). It publishes migrated lines, depth slices, and
detected targets into the project's shared 3D scene, where radar profiles
drape automatically from the site terrain model — far cleaner than raw GPS
elevations. A velocity model from [Bifrost](bifrost.html) in the same
project can drive Midgard's depth conversion directly, and
[Niflheim](niflheim.html)'s conductivity maps render beneath the radar
profiles for joint interpretation.

## Availability

Midgard is commercially licensed as part of the Yggdrasil suite (Windows and
Linux). Contact **[joel@aesirmt.com](mailto:joel@aesirmt.com)** for
licensing and installers.

[← Back to the suite overview](yggdrasil.html)
