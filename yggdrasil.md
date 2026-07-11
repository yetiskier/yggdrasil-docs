---
title: The Yggdrasil platform
description: Geophysical processing suite — one project, one 3D scene, one license.
---

<p align="center">
  <img src="assets/img/Yggdrasil_logo.png" alt="Yggdrasil logo" width="220">
</p>

# The Yggdrasil suite

Yggdrasil is a commercial geophysical processing platform: a shared desktop
shell plus independently-licensed processing packages ("realms", each named
for a realm of Norse cosmology) that share **one project format, one 3D
scene, and one license file**. Buy the package you need; the shell is the
same, and every data type you add later lands in the same project and the
same scene.

![ERT inverted sections and GPR radar curtains under a translucent DEM + aerial-photo basemap in the shared 3D scene](assets/img/centerville_scene_full.png)

*One project, one scene: seven inverted ERT sections and dozens of migrated
GPR radar curtains from the Centerville site, rendered together beneath the
translucent DEM + aerial-photo basemap.*

## The platform

- **One project format.** A project is a plain, self-contained directory:
  immutable inputs, reproducible derived products, a versioned manifest, and
  an append-only processing history that records every step with who, when,
  and what parameters. Archive it, hand it to a client, open it years later —
  the directory itself is the format; there is no proprietary archive.
- **One 3D scene.** Every package publishes into the same scene graph — radar
  curtains, resistivity sections and volumes, EM conductivity surfaces,
  boreholes, electrode layouts, detected targets — rendered together with a
  shared camera, per-quantity colour scales, and vertical exaggeration.
  Saved views persist with the project.
- **Basemap and DEM integration.** One command downloads an elevation model
  and aerial photo for a project's footprint and drapes them in the scene.
  Radar curtains and electrode layouts take their elevations from the project
  DEM; projects can be georeferenced by local anchor, GPS fixes, or a
  projected CRS (EPSG).
- **Per-data-type processing panels.** The shell shows the processing panels
  relevant to the data a project actually contains — a GPR-only project
  presents GPR tools, an EM+ERT project presents both — and each panel is the
  same form-based GUI the package offers standalone. Every processing setting
  is a labelled widget; nothing is config-file-only.
- **Cross-package workflows.** Packages exchange data through the project,
  not through each other: a velocity volume from Bifrost drives Midgard's
  depth migration; Niflheim's conductivity grids drape under Midgard's
  migrated lines at a physically honest effective depth.
- **Windows and Linux.** The full suite — CLI, GUI, and 3D scene — runs on
  both platforms.

## The realms

<table>
<tr>
<td width="110" align="center"><a href="mimir.html"><img src="assets/img/Mimir_logo.png" alt="Mimir logo" width="90"></a></td>
<td><strong><a href="mimir.html">Mimir — Electrical Resistivity Tomography</a></strong><br>
DC-resistivity and IP: Syscal Pro and BERT-format input, interactive QC and
bad-point editing, GPS/DEM georeferencing, and a native 2D/3D Gauss-Newton
inversion on an in-house triangular mesh.</td>
</tr>
<tr>
<td align="center"><a href="bifrost.html"><img src="assets/img/Bifrost_logo.png" alt="Bifrost logo" width="90"></a></td>
<td><strong><a href="bifrost.html">Bifrost — Borehole GPR Tomography</a></strong><br>
Crosshole traveltime tomography in 2D and 3D — plus arbitrary acquisition
geometries (transducer rings, free-form layouts) — with first-break picking,
ZOP analysis, synthetic resolution testing, and time-lapse comparison.</td>
</tr>
<tr>
<td align="center"><a href="midgard.html"><img src="assets/img/Midgard_logo.png" alt="Midgard logo" width="90"></a></td>
<td><strong><a href="midgard.html">Midgard — Surface GPR</a></strong><br>
Near-surface common-offset GPR: MALA, Sensors &amp; Software, and GSSI input,
GPS geolocation, a reorderable processing pipeline, Kirchhoff/Stolt
migration, automatic target detection, and 3D fence diagrams.</td>
</tr>
<tr>
<td align="center"><a href="niflheim.html"><img src="assets/img/Niflheim_logo.png" alt="Niflheim logo" width="90"></a></td>
<td><strong><a href="niflheim.html">Niflheim — EM Ground Conductivity</a></strong><br>
Frequency-domain EM (Geonics EM31-class instruments): NMEA geolocation,
drift/despike/detrend processing, calibration overrides, map gridding, and
anomaly detection.</td>
</tr>
</table>

## Licensing

Yggdrasil is commercially licensed, per package. Licensing works offline —
a signed license file, no network required in the field — and each package
is independently sellable: a Mimir-only customer gets the full shell with
Mimir active, and can unlock other realms later.

For licensing, pricing, and installers (Windows installer and Linux),
contact **[joel@aesirmt.com](mailto:joel@aesirmt.com)**.

---

*Yggdrasil is proprietary software by Aesir Consulting LLC.*

[← Back to the landing page](index.html)
