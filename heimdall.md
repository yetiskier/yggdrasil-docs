---
title: Heimdall
description: Seismic refraction P-wave velocity (Vp) imaging of the near surface.
---

<p align="center">
  <img src="assets/img/Heimdall_logo.png" alt="Heimdall logo" width="240">
</p>

# Heimdall — Seismic Refraction

**First-arrival traveltime interpretation: P-wave velocity imaging of the near
surface from a refraction spread.**

> Named for **Heimdall**, watchman of the gods and keenest of hearing — he
> catches the first faint sound. Refraction interpretation lives or dies on the
> first break.

Heimdall turns picked first arrivals into a P-wave velocity (`Vp`) model of the
near surface — either as layer models or as a smooth tomographic section. Read
SEG-2, SEG-Y, or SU field records, pick the first breaks, and interpret them
two complementary ways, from a CLI, a desktop GUI, or as a panel in the
Yggdrasil shell.

## What refraction is for

Fire an impulsive source (a sledgehammer on a plate, a weight drop) into the
ground and record the arrivals on a line of geophones. Beyond a crossover
distance, the **first arrival** at each geophone is a **head wave** critically
refracted along a deeper, faster layer. The move-out of those first breaks —
traveltime versus offset — encodes the `Vp` structure and the depth to each
refractor.

Refraction `Vp` is the go-to method for:

- **Depth to bedrock** — the classic refraction target, from the soil-to-rock
  velocity contrast.
- **Water table** — the sharp `Vp` jump into saturated ground.
- **Rippability** — bedrock velocity keys directly into excavation-effort charts.
- **Void, fault, and weathered-layer mapping** — lateral velocity anomalies and
  offsets in the refractor.

## Two interpretation methods

Heimdall turns first breaks into `Vp` two ways from the same picks:

- **Classic layer methods** — the intercept-time and **Generalized Reciprocal
  Method (GRM)** fit the direct and head-wave branches of a reversed spread for
  true layer velocities and **dipping / undulating interface depths**, giving a
  layered refraction model.
- **Refraction tomography** — a regularized inversion on a velocity grid gives a
  smooth, gridded `Vp` section that captures gradual velocity change and lateral
  variation the layer models cannot.

Use them together: the layer model gives crisp interface depths, and the
tomogram shows the gradients and lateral structure between them.

![Refraction tomography P-wave velocity section (synthetic illustration)](assets/img/heimdall_vp_section.png)

*Refraction tomography `Vp` section. Synthetic illustration.*

## Workflow

1. **First-break picking** — automatic picking (STA/LTA and AIC) per gather or
   across the whole line, then click on the gather to refine the nearest
   receiver's pick.
2. **Traveltimes** — assemble forward and reverse traveltime–offset sets from
   the picks.
3. **Interpretation** — run intercept-time / GRM layer inversion, refraction
   tomography, or both.
4. **2D Vp section** — the recovered velocity model, with the traveltime misfit
   reported.

## Supported formats

Native readers for the standard engineering-seismograph formats, with explicit
endianness:

| Format | Extensions | Notes |
|---|---|---|
| **SEG-2** | `.dat` `.sg2` `.seg2` | The engineering-seismograph format (Geometrics, Seistronix); reads receiver/source locations and sample interval. |
| **SEG-Y** | `.sgy` `.segy` | rev1; IBM/IEEE float and int sample formats. |
| **SU** | `.su` | Seismic Unix. |

## One spread, two methods

Seismic refraction (Heimdall) and MASW ([Mjölnir](mjolnir.html)) run on the
**same field records**. Acquire one seismic spread and get both refraction
P-wave velocity (`Vp`, Heimdall) and surface-wave shear velocity (`Vs`,
Mjölnir) — and together `Vp`/`Vs` and Poisson's ratio, a powerful joint
constraint on saturation and material properties. The two realms group under a
**Seismic** category in the Yggdrasil shell and share the imported gather.

## In the Yggdrasil shell

Heimdall publishes `Vp` sections and traveltime sets into a project's shared 3D
scene, draped against the project DEM alongside the site's other geophysics.
Every figure exports through Core's shared exporter, and the `Vp` section
registers on the active project. Every processing setting is a labelled widget
in the GUI — nothing is config-file-only.

## Availability

Heimdall is commercially licensed as part of the Yggdrasil suite (Windows and
Linux). Contact **[joel@aesirmt.com](mailto:joel@aesirmt.com)** for licensing
and installers.

[← Back to the suite overview](yggdrasil.html)
