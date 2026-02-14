---
title: "Data-Driven Turbulence Transition Modeling via FIML"
excerpt: "Developing a Galilean-invariant algebraic transition model based on the Spalart-Allmaras (SA) model using Field Inversion and Symbolic Regression."
collection: #
mathjax: true
---

## 🔍 Research Objective
[cite_start]The primary goal is to overcome the limitations of existing 3D transition models, such as high computational costs (e.g., $SST-\gamma-Re_{\theta}$) and the lack of physical consistency regarding Galilean invariance[cite: 464, 469].

## 🛠️ Methodology & Innovations

* **Algebraic SA-based Model**
  [cite_start]Designed a 1-equation based algebraic transition model to significantly reduce computational overhead compared to multi-equation transport models[cite: 474, 475].
  
* **Field Inversion & Symbolic Regression (FISR)**
  * [cite_start]**Field Inversion:** Utilized adjoint-based flow analysis to invert optimal correction fields ($\beta$) that minimize discrepancies between high-fidelity LES data and RANS predictions[cite: 255, 607].
  * [cite_start]**Symbolic Regression:** Derived explicit and interpretable equations from inverted fields to capture complex flow physics without the 'black-box' limitations of neural networks[cite: 257, 259].

* **3D Flow Indicators (Novelty)**
  [cite_start]Introduced Galilean-invariant features to accurately detect crossflow transitions in rotating systems like rotors[cite: 588, 615]:
  * **Vortex Stretching:** $\omega_{i} S_{ij} \omega_{j}$ (captures enstrophy production).
  * **Pressure-Vorticity Alignment:** $\frac{\omega \cdot \nabla P}{|\omega||\nabla P|}$ (detects directional misalignment due to crossflow).

---

## 🧪 Key Mathematical Model

The derived algebraic expression for the correction field $\beta$ is represented as:

$$
\beta = 0.83 \tanh \left( 0.0513 \log \left( \frac{\tilde{\nu}}{\nu} \right) + 1 \right) \cdot (Re_{\Omega} - Re_{c}) + 1.03 \tanh(13.01 \cdot \omega_{i} S_{ij} \omega_{j}) \cdot \mathcal{F}_{3D}
$$

---

## 🚧 Under Construction
Detailed visualization of the transition flow fields and documentation for the Symbolic Regression process will be updated soon.