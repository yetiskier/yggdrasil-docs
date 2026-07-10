---
title: Mimir
description: Electrical Resistivity Tomography — DC-resistivity and IP processing.
---

<p align="center">
  <img src="assets/img/Mimir_logo.png" alt="Mimir logo" width="200">
</p>

# Mimir — Electrical Resistivity Tomography

**DC-resistivity and induced-polarization (IP) processing for the Yggdrasil
suite.**

> Named for **Mimir**, the well of wisdom at the root of Yggdrasil, whose
> waters the Æsir drink to see beneath the surface of things. ERT looks
> beneath the ground by the same principle — measuring how far a current
> soaks into the earth to reveal the water, salt, clay, and voids the
> surface hides.

Mimir reads ERT survey files, computes apparent resistivity from
array-specific geometric factors (Wenner, Schlumberger, dipole-dipole),
provides interactive QC and editing, runs a native Gauss-Newton inversion to
a 2D section or 3D volume, and publishes the results into a Yggdrasil
project's shared 3D scene.

![Inverted resistivity section](assets/img/centerville_inverted.png)

*Inverted section with confidence-alpha shading — cells the data can't
resolve fade out.*

## Instrument and format support

- **IRIS Syscal Pro `.PRO` and ProsysII `.bin`** binary files, read natively
  — no export step through third-party software required. Placeholder
  elevations are snapped to real peg elevations when available.
- **BERT / unified `.dat`** — 2D or 3D electrode layouts with
  apparent-resistivity and per-datum error columns.

## QC and data editing

- **Auto-QC**: apparent-resistivity clip range, a per-level spike filter,
  reciprocal-pair error rejection, and an RMS-misfit trim pass. Runs
  headless from the CLI, writing an edited survey file plus a replayable
  edits sidecar so every removal is documented and reversible.
- **Interactive bad-point picker**: per-level profile and pseudosection
  views, click-to-toggle, rubber-band bulk select, full undo/redo — over
  the same filters, in the GUI's Edit Data tab.

## Georeferencing

Map electrode numbers to sparse GPS fixes (two or more, any subset — three
or more handles bent lines); untagged electrodes interpolate by tape
chainage. Electrode elevations can be sampled from the project's basemap
DEM, which is downloaded automatically if the project doesn't have one yet.
Per-segment tape-vs-GPS mismatch warnings flag layout errors early.

## Mesh and inversion

The inversion mesh is a **native triangular mesh** built in-house: graded
surface-parallel layers that follow topography and blend to a flat bottom at
the chosen investigation depth, with lateral padding and smoothing. The
solver is a Gauss-Newton loop on log-resistivity with a first-difference
smoothness operator, a physically-motivated error model, data-error
weighting, and an adjustable vertical/horizontal smoothing ratio. Inversion
stops when the data are fit to within their stated errors (χ² target).

Sections carry a **coverage-based confidence fade**: cells the data cannot
resolve are rendered transparent rather than presented as fact.

![Cross-validation against an independent reference implementation](assets/img/centerville_compare.png)

*The native engine is cross-validated against an independent open-source
reference implementation on real field surveys — here a Wenner line, model
log-space correlation 0.958. The third panel fades where data coverage is
low.*

## GUI

![Mimir GUI](assets/img/mimir_gui.png)

Every setting is a labelled widget grouped by tab (Survey / QC / Mesh /
Inversion / IP), with tooltips throughout. Runs execute in the background so
the interface never blocks. The same window embeds as a panel inside the
Yggdrasil shell — any project containing ERT data surfaces Mimir
automatically.

## Scene publishing

One command publishes the electrode layout, pseudosection, and inverted
section or volume into a Yggdrasil project, where they render in the shared
3D scene alongside GPR and EM layers, draped on the project topography.

## Availability

Mimir is commercially licensed as part of the Yggdrasil suite (Windows and
Linux). Contact **[joel@aesirmt.com](mailto:joel@aesirmt.com)** for
licensing and installers.

[← Back to the suite overview](index.html)
