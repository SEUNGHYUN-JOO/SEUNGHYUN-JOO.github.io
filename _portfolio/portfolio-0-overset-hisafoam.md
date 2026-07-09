---
title: "overset-hisafoam: Overset & Rotor Extensions for the HiSA Density-Based Solver"
excerpt: "Overset (chimera) support for the coupled density-based HiSA solver on ESI OpenFOAM: steady SRF rotor analyses with a one-shot stencil, unsteady rigid blade motion with per-blade cyclic pitch/flap, high-order (3rd/5th) CWENO reconstruction with AUSM+up / AUSMPW+ pointwise fluxes, and an OpenFOAM v2606 overset backport. Validated on the Caradonna–Tung rotor."
collection: portfolio
---

[![GitHub](https://img.shields.io/badge/GitHub-overset--hisafoam-181717?logo=github)](https://github.com/SEUNGHYUN-JOO/overset-hisafoam)

## 🔍 Project Overview
[HiSA](https://hisa.gitlab.io/) is a density-based, coupled (GMRES/LU-SGS)
compressible solver for OpenFOAM — but OpenFOAM's native overset machinery
works through segregated `fvMatrix` solves, so it never engages in HiSA's
coupled system. **overset-hisafoam** bridges that gap and turns HiSA into a
rotorcraft-capable overset solver:

- **Explicit fringe coupling** for the coupled system: fringe/hole cell
  residuals are blanked before each linear solve, donor interpolation is
  triggered through the boundary-condition evaluation, and the conservative
  variables are re-synchronised thermodynamically on the fringe.
- **`srfOversetFvMesh`** — single-rotating-frame (absolute-velocity ALE
  formulation, Abuhanieh 2024) combined with the overset framework; the
  component meshes are static in the rotating frame, so the overset stencil
  is assembled **once**. Steady hover analyses at a fraction of the cost of
  time-accurate rotation.
- **`cyclicBladeMotion`** — unsteady rigid blade motion
  `R_shaft(ωt) ∘ R_flap(β(ψ)) ∘ R_pitch(θ(ψ))` with per-blade azimuth phase
  ψ₀, i.e. collective + cyclic pitch and coning + cyclic flapping, driven per
  blade cellZone through `multiSolidBodyMotionSolver` +
  `dynamicOversetFvMesh` (dual-time integration, ~1° of azimuth per step).
- **High-order reconstruction** (`libhisaWENO`): UCNS3D-style k-exact CWENO,
  formally verified to 3rd (`wenoDegree 2`) and 5th (`wenoDegree 4`) order on
  the isentropic-vortex benchmark; genuinely high-order `hoWENO` flux with
  multiple face Gauss points and pointwise **AUSM+up** or **AUSMPW+**
  (Kim–Kim–Rho 2001) Riemann fluxes, plus an **eMLP-VC** region-based limiter
  option; SRF-aware and parallel (multi-layer halo stencils).
- **OpenFOAM v2606 overset backport** — the v2606 robustness fixes to the
  `inverseDistance` cell–cell stencil (fringe-to-fringe donor cascade
  prevention, empty-stencil demotion), backported to v2512 for thin-blade
  overset topologies.
- **Case tooling** — PLOT3D → OpenFOAM component-mesh conversion and one-shot
  generators for the steady SRF overset and unsteady cyclic cases, consuming
  the meshes produced by
  [pyhyp-rotor-overset-generator]({{ '/portfolio/portfolio-1-pyhyp-rotor-overset/' | relative_url }}).

## ✅ Validation status
| Case | Configuration | Result |
|---|---|---|
| Static cylinder (M ≈ 0.2) | `staticOversetFvMesh`, laminar | Physical solution; stagnation pressure & peak velocity match theory |
| Caradonna–Tung hover (θ = 8°, M_tip = 0.439) | steady SRF overset, 6.4M cells (y+ ≈ 1 hex components + Cartesian background), SA | Clean OGA (63k fringe cells), monotone residual convergence |
| Same rotor, conformal single mesh | pyHyp BL + graded far field, SRF | Cross-check track, 300 iterations |
| Same rotor, unsteady | `cyclicBladeMotion` (1°/Δt, cyclic pitch & flap), dual-time backward, 7.0M cells | Rotating-blade overset stepping verified |

## 🔧 Engineering notes
The README documents the full production checklist learned during
development — overset patch/field dictionary pitfalls, why GAMG must be
replaced by PBiCGStab on overset-extended matrices, dual-time settings, and
a built-in AUSM `sqrt`-argument diagnostic guard that pinpoints corrupted
overset states by cell/face location.

GPL-3.0 — built on HiSA (CSIR / O. Oxtoby, J. Heyns) and ESI OpenFOAM.
