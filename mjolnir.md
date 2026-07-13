---
title: Mjölnir
description: MASW surface-wave shear-velocity (Vs) imaging of the near surface.
---

<p align="center">
  <img src="assets/img/Mjolnir_logo.png" alt="Mjölnir logo" width="200">
</p>

# Mjölnir — MASW / Surface Waves

**Multichannel Analysis of Surface Waves: shear-wave velocity imaging of the
near surface from a hammer strike.**

> Named for **Mjölnir**, Thor's hammer — MASW is a hammer-source method. The
> strike is the seismic source, and the ground rings back in surface waves.

Mjölnir turns a multichannel seismic record into a shear-wave velocity (`Vs`)
model of the ground — a direct, non-invasive proxy for soil stiffness. Read
SEG-2, SEG-Y, or SU field records, image the surface-wave dispersion, pick the
curve, invert for a layered `Vs` profile, and stitch a 2D `Vs` section — from a
CLI, a desktop GUI, or as a panel in the Yggdrasil shell.

## What MASW is for

A seismic record from an impulsive source (a sledgehammer on a plate) is
dominated by **Rayleigh surface waves**, which are *dispersive*: each frequency
travels at a phase velocity set by the shear-wave velocity of the ground down
to roughly half its wavelength. Transform the record into a
frequency–phase-velocity image, pick the dispersion curve, and invert it for a
layered `Vs(depth)` model.

`Vs` is the standard measure of near-surface stiffness, so MASW is the method of
choice for:

- **`Vs30` and seismic site classification** — the code-driven average shear
  velocity in the top 30 m for building-code site class and ground-motion work.
- **Geotechnical site characterization** — soil stiffness for foundation and
  settlement design.
- **Depth to bedrock and soft-zone detection** — mapping the stiffness contrast
  between soil and rock, and finding weak or loose zones.
- **Liquefaction screening** — low-`Vs` saturated soils flagged from the section.

## Workflow

1. **Dispersion imaging** — transform each shot gather into a
   frequency–phase-velocity image (phase-shift and slant-stack methods).
2. **Curve picking** — auto-pick the fundamental mode, then click on the image
   to refine the curve; higher modes are supported for deeper resolution.
3. **Layered Vs inversion** — invert the picked curve for a layered `Vs(depth)`
   model, with the data misfit reported.
4. **2D Vs section** — roll the spread along the line and stitch the 1D columns
   into a pseudo-2D `Vs` section.

![Surface-wave dispersion image with the picked fundamental-mode curve (synthetic illustration)](assets/img/masw_dispersion.png)

*Dispersion image with a picked fundamental-mode curve. Synthetic illustration.*

## Supported formats

Native readers and writers for the standard engineering-seismograph formats,
with explicit endianness and round-trip export:

| Format | Extensions | Notes |
|---|---|---|
| **SEG-2** | `.dat` `.sg2` `.seg2` | The engineering-seismograph format (Geometrics, Seistronix); reads receiver/source locations and sample interval. |
| **SEG-Y** | `.sgy` `.segy` | rev1; IBM/IEEE float and int sample formats. |
| **SU** | `.su` | Seismic Unix. |

## One spread, two methods

MASW (Mjölnir) and seismic refraction ([Heimdall](heimdall.html)) run on the
**same field records**. Acquire one seismic spread and get both surface-wave
shear velocity (`Vs`, Mjölnir) and refraction P-wave velocity (`Vp`,
Heimdall) — and together `Vp`/`Vs` and Poisson's ratio, a powerful joint
constraint on saturation and material properties. The two realms group under a
**Seismic** category in the Yggdrasil shell and share the imported gather.

## In the Yggdrasil shell

Mjölnir publishes `Vs` profiles and sections into a project's shared 3D scene,
draped against the project DEM alongside the site's other geophysics. Every
figure exports through Core's shared exporter, and the `Vs` section registers
on the active project for joint interpretation. Every processing setting is a
labelled widget in the GUI — nothing is config-file-only.

## Availability

Mjölnir is commercially licensed as part of the Yggdrasil suite (Windows and
Linux). Contact **[joel@aesirmt.com](mailto:joel@aesirmt.com)** for licensing
and installers.

[← Back to the suite overview](yggdrasil.html)
