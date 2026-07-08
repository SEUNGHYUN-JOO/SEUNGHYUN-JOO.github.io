---
title: "pyhyp-rotor-overset-generator: Open-Source Overset Mesh Generation for Rotors"
excerpt: "Solver-agnostic structured overset (chimera) mesh generation for rotors: wall-resolved (y+ ≈ 1) blade boundary-layer meshes from a plain-text planform table, full-rotor replication, and matched Cartesian background grids. Released on GitHub with a Zenodo DOI."
collection: portfolio
---

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21257648.svg)](https://doi.org/10.5281/zenodo.21257648)
[![GitHub](https://img.shields.io/badge/GitHub-pyhyp--rotor--overset--generator-181717?logo=github)](https://github.com/SEUNGHYUN-JOO/pyhyp-rotor-overset-generator)

## 🔍 Project Overview
Open-source toolchain that turns a **plain-text per-section planform table**
(r/R, chord, twist about 0.25c, LE position, airfoil) into a complete overset
(chimera) mesh system for rotor CFD:

- **Blade component mesh** — a watertight "closed-sock" structured surface
  marched into a wall-resolved (y+ ≈ 1) hexahedral boundary layer with
  [pyHyp](https://github.com/mdolab/pyhyp) (typical mean non-orthogonality ~2°)
- **Full rotor** — automatic replication of the blade volume about the rotor
  axis (`nBlades`)
- **Background mesh** — structured Cartesian grid with a rotor refinement box
  (spacing given in tip chords), growing geometrically outward
- Output is plain **PLOT3D** (+ ParaView VTK export), so the meshes are
  solver-agnostic.

<img src="{{ '/assets/images/portfolio-1-pyhyp/surface.png' | relative_url }}"
     style="width:100%; height:auto; display:block;">
<img src="{{ '/assets/images/portfolio-1-pyhyp/rotor_volume_slice.png' | relative_url }}"
     style="width:100%; height:auto; display:block;">

## ⚙️ Key Features

### Non-degenerate closed-sock topology
pyHyp's normal-consistency check rejects any collapsed cap edge, so blade
tips are closed with **Coons-TFI caps** whose four edges are exact point
subsets of the blade perimeter (leading-edge nose arc / surfaces / blunt-TE
seal) — the marcher sees only supported node topologies. Optional
`capDome` rounds the tip cap.

### Robust real-airfoil support
Selig and Lednicer coordinate files (e.g. straight from the UIUC database)
are auto-detected, resampled with a cubic spline in √x space and noise-filtered,
with the leading-edge point spacing automatically scaled to the estimated
nose radius.

### Overset-aware spacing control
`autoMatch` solves the geometric-series design problem so the outermost
wall-normal blade cell lands just below the background refinement spacing —
the classic overset donor-quality rule — validated against marched volumes
to within ~2%.

<img src="{{ '/assets/images/portfolio-1-pyhyp/rotor_volume.png' | relative_url }}"
     style="width:100%; height:auto; display:block;">
<img src="{{ '/assets/images/portfolio-1-pyhyp/background_volume.png' | relative_url }}"
     style="width:100%; height:auto; display:block;">

## 📦 Examples & Validation
Four fully-worked examples ship with the repository — the Caradonna–Tung
hover rotor, a tapered/swept blade with an airfoil transition, a NACA 23012
blade, and a UH-60-style blade using the real Sikorsky SC1095 section — all
marching to completion with final pyHyp Min Quality ≈ 0.42.

## 🔗 Links
- **GitHub**: [SEUNGHYUN-JOO/pyhyp-rotor-overset-generator](https://github.com/SEUNGHYUN-JOO/pyhyp-rotor-overset-generator)
- **DOI**: [10.5281/zenodo.21257648](https://doi.org/10.5281/zenodo.21257648) — please cite when used
- License: MIT
