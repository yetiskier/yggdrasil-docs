---
title: Bifrost
description: Borehole / crosshole GPR traveltime tomography.
---

<p align="center">
  <img src="assets/img/Bifrost_logo.png" alt="Bifrost logo" width="280">
</p>

# Bifrost — Borehole GPR Tomography

**Crosshole ground-penetrating-radar processing** — first-break picking, 2D
and 3D traveltime tomography, zero-offset-profile (ZOP) velocity/porosity
analysis, synthetic resolution testing, an interactive 3D volume viewer, and
time-lapse change detection — driven by a small YAML config, from a CLI or a
desktop GUI.

> Named for **Bifrost**, the rainbow bridge between worlds in Norse
> mythology. Every ray in a crosshole inversion is a bridge between one
> borehole and another; the recovered velocity field is the rainbow left
> behind by thousands of such crossings.

| Synthetic model (input) | 3D inversion (recovered) | 3D velocity scatter | Time-lapse Δvelocity |
|---|---|---|---|
| ![True 3D model](assets/img/model_3d_true.png) | ![3D inversion depth slices](assets/img/inversion_3d_slices.png) | ![3D velocity scatter](assets/img/scatter_3d.png) | ![Time-lapse difference](assets/img/timelapse_diff.png) |

*A reproducible synthetic 4-borehole site: the planted low-velocity block
(first), the volume the inversion recovers from that geometry (second), the
same volume as a 3D scatter with velocity-scaled opacity (third), and the
per-cell velocity change between two surveys (fourth).*

## A task-focused workflow

The desktop app is built around two obvious starting points:

- **Open GPR data…** — load raw crosshole data (Sensors & Software `.dt1`/
  `.hd`, MALA/RAMAC `.rd3`/`.rd7`+`.rad`), auto-pick first breaks, then invert.
- **Open picks CSV…** — already have first-arrival picks from other
  software? Load the CSV directly and invert — no raw data, no re-picking.
  Column headers are matched tolerantly (case/punctuation/synonyms), so
  common exports load as-is, e.g. Sensors & Software's
  `Tx X (m), Tx Z (m), Rx X (m), Rx Z (m), Time (ns)`; the traveltime unit
  (ns/µs/ms/s) is auto-detected from the header.

Either path lands you at the same short screen: a data summary and geometry
preview, a compact run-settings panel (grid cell size, velocity bounds,
domain), and one **Invert** button that runs the tomography and shows the
velocity tomogram. Synthetic resolution testing, 3D multi-borehole site
inversion, ZOP profiling, the model painter, and the full config form are all
still there — one level down, in a **Tools** menu — for when you need them.

## Interactive first-break pick editor

Picks are shown directly on the gathers, in-app: click a trace to set or
adjust its pick, undo/redo across the whole editing session, step through
gathers one at a time, and re-run auto-pick on demand if you want a fresh
starting point before touching anything by hand. Edited picks feed straight
into the inversion — no export/re-import round trip.

## Automatic QC on import

Every pick is checked against a hard physical limit — apparent velocity
(straight-line distance / traveltime) can never exceed the speed of light —
on the way in, whether it came from raw picking or a pre-picked CSV.
Picks that fail (a typo'd coordinate, a corrupted row, a non-positive
traveltime) are dropped automatically with a clear report of what was
rejected and why, so one bad row in an imported file can't distort an
inversion.

## Publication-ready outputs, on every run

Every inversion writes three figures automatically, no extra steps:

1. **Velocity + rays** — the velocity tomogram with the final-model bent
   raypaths overlaid.
2. **Velocity + confidence** — the same field with each cell's opacity
   scaled by ray coverage, so poorly-resolved cells fade toward a neutral
   background instead of implying confidence the data doesn't support.
3. **Raypaths** — the ray-coverage map with the raypaths on their own.

Sections render in the standard shallow-at-top, deep-at-bottom orientation
regardless of the underlying elevation convention, sized and cropped so the
panel fills the figure, with a secondary depth axis in feet alongside the
primary metric one.

![Crosshole GPR velocity tomogram with raypaths (field data)](assets/img/bifrost_crosshole_field_example.png)

*Crosshole GPR velocity tomogram with raypaths (field data) — one of the
three figures generated automatically on every inversion run.*

## Capabilities

- **First-break picking** — automatic picking plus the interactive editor
  above, for tomography and ZOP gathers.
- **2D crosshole tomography** — a single borehole pair inverted to a
  velocity panel.
- **3D multi-borehole site inversion** — combine many borehole pairs into
  one velocity volume; choose which holes to include per run.
- **ZOP velocity / porosity** vs depth.
- **Synthetic resolution tests** — forward-model a known model on your real
  acquisition geometry, invert it, and see what that geometry can and cannot
  resolve — before you drill or trust an anomaly. A model painter lets you
  draw the test model by hand.
- **Interactive 3D viewer** — spin the recovered volume in the GUI; point
  opacity constant, proportional to velocity, or inverse (making slow
  anomalies pop).
- **Time-lapse comparison** — quantitative Δvelocity between two surveys,
  with automatic regridding when acquisitions don't share an exact grid.
- **Per-trace QC** — crop line ends, or exclude individual bad receiver
  depths inside a line, on top of the automatic physical-plausibility check.

![2D crosshole inversion](assets/img/inversion_2d.png)

*A single borehole pair in 2D: a known model (left — a slow box and a fast
disc) forward-modelled through the pair geometry and inverted with the
native engine (right). The box and disc come back in the right place; the
vertical smearing is the two-hole geometry's resolution limit, not the
engine.*

## Any geometry, not just boreholes

The acquisition layout is configurable:

- **Crosshole** (default) — the classic two-borehole panel.
- **Ring** — transducers on a circle around a cylinder cross-section: a tree
  trunk, a concrete column, a mine pillar.
- **Arbitrary** — fully free-form source/receiver positions from a CSV, one
  measurement per row.

A domain mask (disk, rectangle, polygon, or convex hull of the transducers)
keeps the physics honest: rays cannot shortcut outside the medium (e.g.
through the air around a cylinder), exterior cells are excluded from the
inversion, and smoothing is cut at the boundary.

## Instrument formats

Sensors & Software (`.dt1`/`.hd`) and MALA / RAMAC (`.rd3`/`.rd7` + `.rad`),
via a pluggable reader registry. Per-trace antenna depths are read from
trace headers where the format provides them, and are fully overridable from
the geometry config where it doesn't.

## The inversion engine

Bifrost ships its own, **fully native** tomography engine: a pure
numpy/scipy eikonal (fast-marching) forward solver — full refraction and
curved rays, not a straight-ray approximation — paired with a matrix-free,
regularized Gauss-Newton inversion (smoothness + damping, parallel across
sources). No compiled extension, so it installs and runs identically on
**Windows and Linux**. Memory stays flat as the model grows, so it scales to
hundreds of sensors per hole. Iteration stops when the picks are fit to
within their stated uncertainty (χ² ≈ 1) — fitting further would be fitting
noise. The engine is validated against an independent open-source reference
implementation, agreeing to ~96–98% on synthetic benchmarks.

## GUI

Two entry points, one Invert button, and a Tools menu for everything else
(see [above](#a-task-focused-workflow)) — with the full config still
available underneath as a labelled-widget form when you need it, plus
bundled runnable examples (File → Open Example), a live log, a figure
browser, and the embedded 3D volume/time-lapse viewer. Bifrost also embeds
as a panel inside the Yggdrasil shell, and its velocity volumes can
directly drive [Midgard](midgard.html)'s depth migration through the shared
project format.

## Availability

Bifrost is commercially licensed as part of the Yggdrasil suite (Windows and
Linux). Contact **[joel@aesirmt.com](mailto:joel@aesirmt.com)** for
licensing and installers.

[← Back to the suite overview](yggdrasil.html)
