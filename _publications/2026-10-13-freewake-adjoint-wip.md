---
title: "A Fully Coupled CFD–Free-Wake Discrete Adjoint for Rotor Design: Retaining Far-Wake Sensitivity"
collection: publications
category: manuscripts
permalink: /publication/2026-freewake-adjoint
date: 2026-10-13
status: 'Work in Progress'
citation: '**Seunghyun Joo**, Kwanjung Yee. "A Fully Coupled CFD–Free-Wake Discrete Adjoint for Rotor Design: Retaining Far-Wake Sensitivity." <i>Work in progress</i>.'
excerpt: 'The CFD residual and the periodic free-wake equilibrium residual are solved as one coupled system in both the primal and the adjoint, so the far wake is modeled cheaply but its design sensitivity is retained.'
---

> 🚧 **Status:** Work in progress. The manuscript is in preparation (working title).
>
> **Authors:** Seunghyun Joo, Kwanjung Yee

## 🔍 Overview
Hybrid CFD–free-wake methods are widely used for rotors because they model the far wake at low cost. In design adjoints, however, the wake is usually **frozen**, and its response to design changes is discarded.

The wake has been frozen mainly because of code structure (the wake is an external input to the CFD), the added cost of a wake adjoint, and the numerical difficulty of differentiating chaotic time-marching hover wakes. Earlier studies found that wake coupling had a small effect on the airloads under their conditions, but its effect on the design sensitivities was not evaluated.

In this work, **the CFD residual and the periodic free-wake equilibrium residual are solved as one coupled system in both the primal and the adjoint**, so the far wake is modeled cheaply but its design sensitivity is retained.

## ✨ Contributions
1. A **discrete adjoint that couples the CFD and free-wake residuals**, including the cross-coupling between the near-blade flow and the wake.
2. **Quantitative evidence** that frozen-wake gradients are inaccurate and that this error **shifts the optimum**.
3. Extension to **forward flight** and to **rotors installed with a fuselage**.

## ✅ Preliminary Results
* **Gradient accuracy:** frozen-wake gradients differ by up to about 60% for the hover chord variables and by 20–25% for the cruise lift sensitivity to root pitch; the trim (pitching-moment) sensitivity differs by a factor of about 7.
* **HART II hover:** coupled optimization raised the figure of merit from **0.689 to 0.727**. The optimum found with a frozen wake has a 0.9% worse torque coefficient, and the coupled gradient at that point is not zero.
* **Rotor with fuselage (ROBIN):** paired comparison of isolated and installed blade designs in hover and forward flight (ongoing).

## 🛠️ Method
* **Near-blade CFD:** [CuDAFLOW]({{ '/portfolio/portfolio-0-cudaflow/' | relative_url }}), an in-house GPU RANS solver (Spalart–Allmaras), with one block per blade.
* **Free wake:** a low-degree-of-freedom free-wake model solved as a periodic equilibrium in the inertial frame.
* **Coupling:** CFD → blade circulation → wake → induced velocity → CFD. A panel model of the fuselage can be added to the coupled system.
* **Coupled adjoint:** includes the off-diagonal coupling terms between the CFD and wake residuals. The CFD adjoint is solved backward in time, the wake adjoint as a periodic equilibrium, and trim is included through a reduced gradient. The usual frozen-wake adjoint is recovered by setting the coupling terms to zero, which allows a fair comparison.

---

## 📊 Validation & Optimization Results
{% include freewake-figures.html %}
