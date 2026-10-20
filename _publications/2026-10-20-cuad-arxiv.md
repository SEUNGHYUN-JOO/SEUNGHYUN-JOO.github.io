---
title: "CuAD: Source-to-Source Automatic Differentiation of CUDA Kernels for Discrete Adjoints in Computational Fluid Dynamics"
collection: publications
category: manuscripts
permalink: /publication/2026-cuad
date: 2026-10-20
status: 'Preprint'
venue: 'arXiv (physics.flu-dyn)'
paperurl: 'https://arxiv.org/abs/2610.26694'
excerpt: 'A source-to-source AD tool that writes tangent and adjoint CUDA kernels whose reverse sweep recomputes instead of storing, compared under one compiler with Clad and Enzyme and applied to a complete transonic Euler adjoint. Preprint: arXiv:2610.26694.'
citation: '**Seunghyun Joo**. (2026). "CuAD: Source-to-Source Automatic Differentiation of CUDA Kernels for Discrete Adjoints in Computational Fluid Dynamics." <i>arXiv preprint</i> arXiv:2610.26694.'
---

[![arXiv](https://img.shields.io/badge/arXiv-2610.26694-b31b1b?logo=arxiv)](https://arxiv.org/abs/2610.26694)
[![GitHub](https://img.shields.io/badge/GitHub-CuAD-181717?logo=github)](https://github.com/SEUNGHYUN-JOO/CuAD)

## 🔍 Overview
Discrete adjoints give the sensitivities that aerodynamic design needs, but they are hard to obtain for flow solvers that run on GPUs. **CuAD** reads CUDA kernels and writes their tangent and adjoint versions as ordinary CUDA source ([project page]({{ '/portfolio/portfolio-6-cuad/' | relative_url }})).

Its reverse mode is organised around the GPU thread. It adopts the convention of CUDA kernels that inputs and outputs do not alias, so intermediate values are recomputed instead of stored. Pure accumulations are differentiated without a tape, and the scalars that a loop carries from one iteration to the next are kept in a fixed thread-local array rather than in the device heap.

## ✅ Highlights
* **What decides the cost of a GPU adjoint.** On a Biot–Savart summation compiled by one compiler, the CuAD adjoint costs about four times the primal at every size up to 16384 vortices. Enzyme reaches the same cost once the source declares `__restrict__`. On the unchanged source, Enzyme's heap cache and Clad's heap tape cost 9 to 4400 times the primal, vary between runs, and Clad fails beyond 8192 vortices.
* **Exact Jacobians in single precision.** Jacobians assembled from the generated tangents keep the adjoint gradients accurate to 1e-6 on a transonic airfoil and 4e-5 on a stiff Burgers problem. Single-precision finite differences give errors of 5e-4 to 4e-2 and of 45 to 75 per cent.
* **A complete 2-D Euler adjoint.** For a transonic NACA 0012, the residual, the wall and far-field boundary conditions and the wall force are differentiated without change to the source. The lift and drag shape sensitivities from the adjoint and from the tangent agree to 1e-13.

---

## 🧪 Selected Results

### Comparison with Clad and Enzyme
<figure>
  <img src="{{ '/assets/images/publication-cuad-arxiv/biot_savart_scaling.png' | relative_url }}" alt="Biot-Savart adjoint cost and device heap of four tools">
  <figcaption>Biot–Savart adjoint of four tools under one compiler: median cost of three runs relative to the primal kernel, and the device heap that the tape or cache of Clad and Enzyme requires.</figcaption>
</figure>

### Transonic NACA 0012 (2-D Euler)
<figure>
  <img src="{{ '/assets/images/publication-cuad-arxiv/euler2d_flow.png' | relative_url }}" alt="Transonic NACA 0012 Mach number and surface pressure">
  <figcaption>Mach number with the sonic line and surface pressure at M = 0.8 and α = 1.25° on a 160 × 64 O-grid.</figcaption>
</figure>
<figure>
  <img src="{{ '/assets/images/publication-cuad-arxiv/euler2d_adjoint.png' | relative_url }}" alt="Lift adjoint and shape sensitivities">
  <figcaption>Lift adjoint and the lift and drag sensitivities to eight Hicks–Henne parameters, from the adjoint (bars) and from the tangent (circles).</figcaption>
</figure>

### Single-precision Jacobians
<figure>
  <img src="{{ '/assets/images/publication-cuad-arxiv/burgers_gradient_error.png' | relative_url }}" alt="Adjoint gradient error against condition number">
  <figcaption>Steady Burgers problem: relative error of the adjoint gradient against the condition number, for single-precision Jacobians from the CuAD tangent and from central differences.</figcaption>
</figure>

### Further applications
<figure>
  <img src="{{ '/assets/images/publication-cuad-arxiv/nozzle_flow.png' | relative_url }}" alt="Nozzle inverse design">
  <figcaption>Inverse design of a transonic nozzle: area, Mach number and pressure of the initial, target and designed geometry, and the adjoint at the initial design.</figcaption>
</figure>
<figure>
  <img src="{{ '/assets/images/publication-cuad-arxiv/vortex_sheet.png' | relative_url }}" alt="Vortex sheet roll-up and sensitivity">
  <figcaption>Unsteady adjoint of a rolling-up vortex sheet behind an elliptically loaded wing: roll-up and the sensitivity of the wake descent.</figcaption>
</figure>
