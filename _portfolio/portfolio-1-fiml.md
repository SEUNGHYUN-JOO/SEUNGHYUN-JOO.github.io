---
title: "Data-Driven Turbulence Transition Modeling via FIML"
[cite_start]excerpt: "Developing a Galilean-invariant algebraic transition model based on the Spalart-Allmaras (SA) model using Field Inversion and Symbolic Regression. [cite: 442, 475]"
collection: portfolio
---

## 🔍 Research Objective
[cite_start]Solving the limitations of existing 3D transition models, such as high computational costs (e.g., $SST-\gamma-Re_{\theta}$ [cite: 472][cite_start]) and lack of physical consistency (Galilean invariance [cite: 469]).

## 🛠️ Methodology & Innovations
* [cite_start]**Algebraic SA-based Model:** Designed a 1-equation based algebraic transition model to reduce computational overhead compared to multi-equation transport models. [cite: 474]
* [cite_start]**Shielding Functions:** Implemented specialized shielding functions ($F_{eff}$) using DDES-based formulations to preserve baseline SA performance in fully turbulent boundary layers. [cite: 498, 508]
* [cite_start]**Field Inversion & Symbolic Regression (FISR):** * Inverted correction fields ($\beta$) to minimize discrepancies between high-precision LES data and RANS predictions. [cite: 255, 607]
    * [cite_start]Derived explicit, interpretable equations using **Symbolic Regression** to capture 3D flow physics. [cite: 257, 546]
* [cite_start]**3D Flow Indicators (Novelty):** Introduced Galilean-invariant features such as **Vortex Stretching** ($\omega_i S_{ij} \omega_j$) and **Pressure-Vorticity Alignment** to accurately detect crossflow transition in rotating systems like rotors. [cite: 554, 615, 620]

## 🚀 Current Status & Goals
* [cite_start]Validated on separation-induced transition (NACA0012). [cite: 291]
* [cite_start]Targeting submission to **Physics of Fluids (PoF)** and presentation at **AIAA SCITECH 2026**. [cite: 304, 328]

## 🚧 Under Construction
Detailed visualization of the sizing sensitivity analysis and documentation will be updated soon.