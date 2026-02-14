---
title: "Data-Driven Turbulence Transition Modeling via FIML"
excerpt: "Developing a Galilean-invariant algebraic transition model based on the Spalart-Allmaras (SA) model using Field Inversion and Symbolic Regression."
collection: portfolio
---

## 🔍 Research Objective
Solving the limitations of existing 3D transition models, such as high computational costs (e.g., $SST-\gamma-Re_{\theta}$) and lack of physical consistency (Galilean invariance).

## 🛠️ Methodology & Innovations
* **Algebraic SA-based Model:** Designed a 1-equation based algebraic transition model to reduce computational overhead compared to multi-equation transport models.
* **Shielding Functions:** Implemented specialized shielding functions ($F_{eff}$) using DDES-based formulations to preserve baseline SA performance in fully turbulent boundary layers.
* **Field Inversion & Symbolic Regression (FISR):** * Inverted correction fields ($\beta$) to minimize discrepancies between high-precision LES data and RANS predictions.
    * Derived explicit, interpretable equations using **Symbolic Regression** to capture 3D flow physics.
* **3D Flow Indicators (Novelty):** Introduced Galilean-invariant features such as **Vortex Stretching** ($\omega_i S_{ij} \omega_j$) and **Pressure-Vorticity Alignment** to accurately detect crossflow transition in rotating systems like rotors.

## 🚧 Under Construction
Detailed visualization of the sizing sensitivity analysis and documentation will be updated soon.