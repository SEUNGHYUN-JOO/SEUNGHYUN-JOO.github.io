---
title: "overset-hisafoam: Overset & Rotor Extensions for the HiSA Density-Based Solver"
excerpt: "Released on GitHub with a Zenodo DOI. Overset (chimera) support for the coupled density-based HiSA solver on ESI OpenFOAM: steady SRF rotor analyses with a one-shot stencil, unsteady rigid blade motion with per-blade cyclic pitch/flap, high-order (3rd/5th) CWENO reconstruction with AUSM+up / AUSMPW+ pointwise fluxes, and an OpenFOAM v2606 overset backport. Exercised end-to-end on the Caradonna–Tung rotor (bring-up level; production validation in progress)."
collection: portfolio
---

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21278074.svg)](https://doi.org/10.5281/zenodo.21278074)
[![GitHub](https://img.shields.io/badge/GitHub-overset--hisafoam-181717?logo=github)](https://github.com/SEUNGHYUN-JOO/overset-hisafoam)

## 🔍 Project Overview

[HiSA](https://hisa.gitlab.io/) is a density-based, coupled (GMRES/LU-SGS)
compressible solver for OpenFOAM. OpenFOAM's native overset machinery works
through segregated matrix solves, so it never engages in HiSA's coupled
system. **overset-hisafoam** bridges that gap and turns HiSA into a
rotorcraft-capable overset solver:

- **Explicit fringe coupling** for the coupled system: fringe/hole cell
  residuals are blanked before each linear solve, donor interpolation is
  triggered through the boundary-condition evaluation, and the conservative
  variables are re-synchronised thermodynamically on the fringe.
- **srfOversetFvMesh** — single-rotating-frame rotor modelling
  (absolute-velocity ALE formulation, Abuhanieh 2024) combined with the
  overset framework; the component meshes are static in the rotating frame,
  so the overset stencil is assembled only once. Steady hover analyses at a
  fraction of the cost of time-accurate rotation.
- **cyclicBladeMotion** — unsteady rigid blade motion composed of the shaft
  rotation, cyclic flapping and cyclic pitch (collective + first-harmonic
  cyclic inputs with a per-blade azimuth phase), driven per blade cellZone
  through multiSolidBodyMotionSolver + dynamicOversetFvMesh with dual-time
  integration (about one degree of azimuth per physical time step).
- **High-order reconstruction** (libhisaWENO): UCNS3D-style k-exact CWENO,
  formally verified to 3rd and 5th spatial order on the isentropic-vortex
  benchmark; a genuinely high-order flux path with multiple face Gauss
  points and pointwise **AUSM+up** or **AUSMPW+** (Kim–Kim–Rho 2001) Riemann
  fluxes, plus an **eMLP-VC** region-based limiter option; SRF-aware and
  parallel (multi-layer halo stencils).
- **OpenFOAM v2606 overset backport** — the v2606 robustness fixes to the
  inverseDistance cell–cell stencil (fringe-to-fringe donor cascade
  prevention, empty-stencil demotion), backported to v2512 for thin-blade
  overset topologies.
- **Case tooling** — PLOT3D to OpenFOAM component-mesh conversion and
  one-shot generators for the steady SRF overset and unsteady cyclic cases,
  consuming the meshes produced by
  [pyhyp-rotor-overset-generator]({{ '/portfolio/portfolio-1-pyhyp-rotor-overset/' | relative_url }}).

## ✅ Validation Status

<table>
  <thead>
    <tr><th>Case</th><th>Configuration</th><th>Result</th></tr>
  </thead>
  <tbody>
    <tr>
      <td>Static cylinder (M ≈ 0.2)</td>
      <td>staticOversetFvMesh, laminar</td>
      <td>Physical solution; stagnation pressure and peak velocity match theory</td>
    </tr>
    <tr>
      <td>Caradonna–Tung hover (θ = 8°, M<sub>tip</sub> = 0.439)</td>
      <td>Steady SRF overset, 6.4M cells (y+ ≈ 1 hex components + Cartesian background), Spalart–Allmaras</td>
      <td>Clean overset assembly (63k fringe cells), monotone residual convergence</td>
    </tr>
    <tr>
      <td>Same rotor, conformal single mesh</td>
      <td>pyHyp boundary layer + graded far field, SRF</td>
      <td>Cross-check track, 300 iterations</td>
    </tr>
    <tr>
      <td>Same rotor, unsteady</td>
      <td>cyclicBladeMotion (1° per step, cyclic pitch and flap), dual-time backward, 7.0M cells</td>
      <td>Rotating-blade overset time stepping verified</td>
    </tr>
  </tbody>
</table>

## 🔧 Engineering Notes

The README documents the full production checklist learned during
development: overset patch and field dictionary pitfalls, why GAMG must be
replaced by PBiCGStab on overset-extended matrices, dual-time settings, and
a built-in diagnostic guard on the AUSM sound-speed argument that pinpoints
corrupted overset states by cell or face location.

GPL-3.0 — built on HiSA (CSIR / O. Oxtoby, J. Heyns) and ESI OpenFOAM.
