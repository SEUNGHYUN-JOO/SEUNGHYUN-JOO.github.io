---
title: "CuAD: Source-to-Source Automatic Differentiation for CUDA"
excerpt: "An open-source, Tapenade-style source-to-source AD compiler for CUDA built on Clang LibTooling. It generates exact forward (tangent) and reverse (adjoint) GPU kernels from the original CUDA source, and powers the discrete adjoint of CuDAFLOW."
collection: portfolio
permalink: /portfolio/portfolio-6-cuad/
---

[![GitHub](https://img.shields.io/badge/GitHub-CuAD-181717?logo=github)](https://github.com/SEUNGHYUN-JOO/CuAD)
[![arXiv](https://img.shields.io/badge/arXiv-2610.26694-b31b1b?logo=arxiv)](https://arxiv.org/abs/2610.26694)

## 🔍 Project Overview
**CuAD** (CUDA Automatic Differentiation) reads CUDA kernels and writes their derivatives as new CUDA source: a **forward (tangent)** companion `f_d` and a **reverse (adjoint)** companion `f_b` for each `__global__` / `__device__` function. Because it differentiates the kernel source itself, every derivative is exact (no finite differences), and the generated kernels run on the GPU like the originals.

CuAD was developed for the exact discrete adjoint of [CuDAFLOW]({{ '/portfolio/portfolio-0-cudaflow/' | relative_url }}), where it differentiates the flux, viscous, and turbulence-model residual kernels.

## 📄 Paper
**CuAD: Source-to-Source Automatic Differentiation of CUDA Kernels for Discrete Adjoints in Computational Fluid Dynamics**, [arXiv:2610.26694](https://arxiv.org/abs/2610.26694) ([publication page]({{ '/publication/2026-cuad' | relative_url }})).

* Under the no-aliasing convention of CUDA kernels, the reverse sweep recomputes instead of storing. On a Biot–Savart summation the CuAD adjoint costs about four times the primal at every size, while the heap-based tapes of Clad and Enzyme (without `__restrict__`) cost 9 to 4400 times the primal.
* For a transonic NACA 0012, the residual, both boundary conditions and the wall force are differentiated without change to the source, and the adjoint and tangent shape sensitivities agree to 1e-13.

<figure>
  <img src="{{ '/assets/images/publication-cuad-arxiv/biot_savart_scaling.png' | relative_url }}" alt="Biot-Savart adjoint cost of CuAD, Clad and Enzyme">
  <figcaption>Biot–Savart adjoint of four tools under one compiler: cost relative to the primal kernel and the device heap required by the tape or cache.</figcaption>
</figure>
<figure>
  <img src="{{ '/assets/images/publication-cuad-arxiv/euler2d_adjoint.png' | relative_url }}" alt="Transonic NACA 0012 lift adjoint and shape sensitivities">
  <figcaption>Transonic NACA 0012: lift adjoint and the lift and drag shape sensitivities from the adjoint (bars) and the tangent (circles).</figcaption>
</figure>

## 🛠️ Key Features
* **Forward and reverse mode**, including calls between user functions (each callee gets its own companion).
* **Activity analysis**: only variables that depend on active inputs are differentiated.
* **Recompute rather than store**: under the convention that a kernel's inputs and outputs do not alias, loops are recomputed in the reverse sweep; only scalars carried between iterations are checkpointed, and pure accumulations (`v = v + e`) need nothing.
* **Thread-local tape**: values that must be restored go to a fixed-size per-thread array, not to the device heap.
* **GPU-safe adjoint accumulation**: `atomicAdd` for shared arrays, plain `+=` for thread-local data.
* **Loops and control flow**: grid-stride loops, per-iteration recomputation, `#pragma unroll`, early exits, `c ? a : b`.
* **C++ constructs**: function templates, default arguments, reference outputs, local pointers and arrays of pointers.
* **Math library**: trigonometric, exponential, power, `atan2`, `hypot`, `copysign`, `cbrt`, and more, in float and double.

## 🆕 Improvements over the Version Bundled in CuDAFLOW
* **Fixes for silently wrong derivatives**, each checked against finite differences: `c ? a : b` (its adjoint was dropped), a one-sided `if` in the middle of a function (the reverse sweep ran in the wrong order), value-returning user functions nested in expressions (adjoint was 0), and `copysign`.
* **Less tape**: pure accumulations need no tape, and recompute loops replay their primal without pushes.
* **Broader language coverage**: templates, default arguments, reference outputs, array parameters, local pointers, early exits, branch-local declarations, bare blocks, `#pragma unroll`, in-place updates of local arrays in loops.
* **More math functions**: `atan2`, `atan`, `asin`, `acos`, `hypot`, `cbrt`, `copysign`, and piecewise-constant `floor` / `ceil` / `round`.

## ✅ Verification
The test suite checks every generated tangent and adjoint against central finite differences and with adjoint dot-product tests (⟨y̅, J ẋ⟩ = ⟨Jᵀ y̅, ẋ⟩):

<table>
  <thead>
    <tr><th>Case</th><th>Check</th></tr>
  </thead>
  <tbody>
    <tr><td>Small kernels (scalar math, loops, overwritten values, device calls, atomic scatter)</td><td>Tangent and adjoint vs. FD, relative error ~1e-11</td></tr>
    <tr><td>CuDAFLOW kernels (conservative-to-primitive, cell volume)</td><td>Tangent FD and adjoint dot test</td></tr>
    <tr><td>Mesh shape optimisation and NACA 0012 inverse design</td><td>Adjoint gradient vs. FD, then converged optimisation</td></tr>
    <tr><td>Spalart–Allmaras field inversion (FIML)</td><td>SA source adjoint dot test; recovers the correction field β</td></tr>
    <tr><td>Loops carrying scalars between iterations (v0.2.1)</td><td>Adjoint vs. FD, relative error ~1e-10</td></tr>
    <tr><td>Transonic NACA 0012, 2-D Euler (paper)</td><td>Adjoint vs. tangent shape sensitivities, 5e-14</td></tr>
  </tbody>
</table>

## 🧪 Technical Skills Demonstrated
* **Languages / tools:** C++17, CUDA, Clang LibTooling (AST analysis and source rewriting)
* **Methods:** Algorithmic differentiation (tangent and adjoint), activity analysis, taping, discrete adjoint methods

GPL-3.0.
