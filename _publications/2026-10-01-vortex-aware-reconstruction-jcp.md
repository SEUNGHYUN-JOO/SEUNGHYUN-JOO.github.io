---
title: "Vortex-Aware Reconstruction Selection for Reducing Vortex Dissipation, Informed by Field Inversion and Symbolic Regression"
collection: publications
category: manuscripts
permalink: /publication/2026-vortex-aware-reconstruction
date: 2026-10-01
status: 'Under Review'
venue: 'Journal of Computational Physics (JCP)'
excerpt: 'A vortex-aware (VA) reconstruction selector that reduces the numerical dissipation of under-resolved vortices in compressible flows while keeping the shock-capturing behavior of the baseline scheme.'
citation: '**Seunghyun Joo**, Yoonpyo Hong, Younghyo Kim, Kwanjung Yee. (2026). "Vortex-Aware Reconstruction Selection for Reducing Vortex Dissipation, Informed by Field Inversion and Symbolic Regression." <i>Under review, Journal of Computational Physics</i>.'
---

> 📝 **Status:** Under review (Journal of Computational Physics). Since the manuscript is not yet published, the formulation is omitted here; this page shows selected numerical examples only.

## 🔍 Overview
Vortices in compressible flows often travel long distances on grids that resolve their cores with only a few cells. Shock-capturing reconstructions tend to treat such under-resolved vortices as discontinuities, and the extra dissipation weakens them over time.

This work proposes a **vortex-aware (VA) reconstruction selector**, informed by **field inversion** and **symbolic regression**, that keeps vortices from decaying while leaving the baseline's shock capturing unchanged. VA works as an add-on to three different baseline reconstructions: **TVD**, **WENO-Z**, and **eMLP-VC**.

## ✅ Highlights
* Better preservation of vortex circulation and vortical structures for all three baselines.
* Shock and shear-layer behavior of the baselines is kept.
* Small additional computational cost.

---

## 🧪 Numerical Examples

### Linear-wave advection
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/01_linear_wave_spatial_convergence_combined.jpg' | relative_url }}" alt="Linear-wave advection grid convergence">
  <figcaption>Grid convergence for linear-wave advection: the baselines and their VA variants keep the design order of accuracy.</figcaption>
</figure>

### Isentropic vortex on an under-resolved grid
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/03_isentropic_vortex_vorticity.jpg' | relative_url }}" alt="Isentropic vortex vorticity and circulation">
  <figcaption>Vorticity and radial circulation of the isentropic vortex on a 20 × 20 grid. Bold titles denote VA variants.</figcaption>
</figure>

### Taylor–Green vortex (subsonic and supersonic)
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/05_tgv_subsonic_supersonic_history.jpg' | relative_url }}" alt="Taylor-Green vortex enstrophy and dissipation history">
  <figcaption>Taylor–Green vortex on 128³: enstrophy at Ma = 0.1 and viscous dissipation rate at Ma = 1.25.</figcaption>
</figure>
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/06_tgv_subsonic_q_isosurfaces.jpg' | relative_url }}" alt="Subsonic Taylor-Green vortex Q isosurfaces">
  <figcaption>Q-criterion isosurfaces of the subsonic Taylor–Green vortex (Ma = 0.1), colored by vorticity magnitude.</figcaption>
</figure>
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/07_tgv_supersonic_q_isosurfaces.jpg' | relative_url }}" alt="Supersonic Taylor-Green vortex Q isosurfaces">
  <figcaption>Q-criterion isosurfaces of the supersonic Taylor–Green vortex (Ma = 1.25), colored by vorticity magnitude.</figcaption>
</figure>

### Stationary shock and steady shock reflection
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/04_stationary_shock_pressure_and_geometry.jpg' | relative_url }}" alt="Stationary shock pressure profiles">
  <figcaption>Pressure along a line through the stationary shock for each baseline and its VA variant.</figcaption>
</figure>
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/20_shock_reflection_convergence.jpg' | relative_url }}" alt="Steady regular shock reflection convergence">
  <figcaption>Steady regular shock reflection: residual histories and density profiles.</figcaption>
</figure>

### Kelvin–Helmholtz instability
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/09_kh_vorticity_and_va_difference.jpg' | relative_url }}" alt="Kelvin-Helmholtz roll-up vorticity">
  <figcaption>Vorticity in one Kelvin–Helmholtz roll-up and its change due to VA for the three baselines.</figcaption>
</figure>

### Shock–vortex interaction
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/10_shock_vortex_schlieren_and_density.jpg' | relative_url }}" alt="Shock-vortex interaction numerical schlieren">
  <figcaption>Shock–vortex interaction: numerical schlieren, enlarged tail, and density profile against a fine-grid reference.</figcaption>
</figure>

### Shock–wedge diffraction
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/16_shock_wedge_t4.jpg' | relative_url }}" alt="Shock-wedge diffraction schlieren and vorticity">
  <figcaption>Shock–wedge diffraction: numerical schlieren (baseline above, mirrored VA result below) and vorticity of the shed vortex.</figcaption>
</figure>

### Two-dimensional blade–vortex interaction (BVI)
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/12_bvi_setup.jpg' | relative_url }}" alt="Two-dimensional BVI configuration">
  <figcaption>Configuration of the two-dimensional blade–vortex interaction: O-grid, leading-edge stations, and vortex release point.</figcaption>
</figure>
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/12_bvi_vortex_core.jpg' | relative_url }}" alt="Incoming vortex of the BVI case">
  <figcaption>The incoming vortex approaching the airfoil, for each baseline and its VA variant.</figcaption>
</figure>
<figure>
  <img src="{{ '/assets/images/publication-va-jcp/11_bvi_surface_pressure_xc002.jpg' | relative_url }}" alt="BVI surface pressure coefficient history">
  <figcaption>Surface pressure coefficient near the leading edge (x/c = 0.02) during the interaction.</figcaption>
</figure>
