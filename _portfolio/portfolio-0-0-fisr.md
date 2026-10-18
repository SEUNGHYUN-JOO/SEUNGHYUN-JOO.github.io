---
title: "Interpretable Data-Driven CFD Modeling via Field Inversion & Symbolic Regression"
excerpt: "Using field inversion (FI) and symbolic regression (SR) to turn high-fidelity data into explicit, closed-form models: a mechanism-separated transition model for RANS (under review, AIAA Journal) and a vortex-aware reconstruction selector for shock-capturing schemes (under review, JCP)."
collection: portfolio
permalink: /portfolio/portfolio-5-fisr/
---

## 🔍 Project Overview
Machine-learned corrections in CFD are often black boxes that are expensive to run and hard to carry over to other solvers. This project uses a two-step **field inversion (FI) → symbolic regression (SR)** approach to obtain **explicit, closed-form models**:

1. **Field inversion** finds the cell-wise correction that best matches high-fidelity or experimental reference data.
2. **Symbolic regression** turns that correction into a compact algebraic expression of local flow features.

The resulting models are interpretable, cheap to evaluate, and simple to implement in other solvers.

---

## 📚 Applications

### 1. Mechanism-Separated Closed-Form Transition Model *(Under Review, AIAA Journal)*
* Separate correction branches for **natural**, **crossflow**, and **separation-induced** transition, added to the Spalart–Allmaras production term.
* No additional transport equations and no neural-network inference.
* Tested on canonical cases, a natural-laminar-flow transport wing, and a hovering rotor; on the rotor it needed about 55% of the wall-clock time of a comparable transport-equation model.
* 📄 [Publication page]({{ '/publication/2026-fisr-transition' | relative_url }}) · [arXiv:2609.24162](https://arxiv.org/abs/2609.24162)

### 2. Vortex-Aware Reconstruction Selection *(Under Review, JCP)*
* Reduces the numerical dissipation of under-resolved vortices in compressible flows.
* Works as an add-on to TVD, WENO-Z, and eMLP-VC reconstructions while keeping their shock-capturing behavior.
* Demonstrated on vortex transport, Taylor–Green vortices, shock–vortex interaction, shock–wedge diffraction, and blade–vortex interaction.
* 📄 [Publication page with numerical examples]({{ '/publication/2026-vortex-aware-reconstruction' | relative_url }})

<figure>
  <img src="{{ '/assets/images/publication-va-jcp/10_shock_vortex_schlieren_and_density.jpg' | relative_url }}" alt="Shock-vortex interaction numerical schlieren">
  <figcaption>Shock–vortex interaction computed with the baselines and their vortex-aware (VA) variants.</figcaption>
</figure>

---

## 🧪 Technical Skills Demonstrated
* **Methods:** Field inversion, symbolic regression, adjoint-based optimization, RANS transition modeling, shock-capturing reconstruction (TVD, WENO-Z, MLP)
* **Applications:** Laminar-to-turbulent transition, vortex-dominated compressible flows, rotor aerodynamics
