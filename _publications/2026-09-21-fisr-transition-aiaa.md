---
title: "Mechanism-Separated Closed-Form Transition Modeling via Field Inversion and Symbolic Regression"
collection: publications
category: manuscripts
permalink: /publication/2026-fisr-transition
date: 2026-09-21
status: 'Under Review'
venue: 'AIAA Journal'
paperurl: 'https://arxiv.org/abs/2609.24162'
excerpt: 'A closed-form, mechanism-separated laminar-to-turbulent transition model for the Spalart–Allmaras equation, built with field inversion and symbolic regression. Preprint: arXiv:2609.24162.'
citation: '**Seunghyun Joo**, Younghyo Kim, Kwanjung Yee. (2026). "Mechanism-Separated Closed-Form Transition Modeling via Field Inversion and Symbolic Regression." <i>Under review, AIAA Journal</i>. arXiv:2609.24162.'
---

[![arXiv](https://img.shields.io/badge/arXiv-2609.24162-b31b1b?logo=arxiv)](https://arxiv.org/abs/2609.24162)

> 📝 **Status:** Under review (AIAA Journal). The preprint is available on [arXiv](https://arxiv.org/abs/2609.24162).

## 🔍 Overview
This work proposes a laminar-to-turbulent transition model that covers **natural**, **crossflow**, and **separation-induced** transition, with a separate correction branch for each mechanism.

* **Data-driven but closed-form:** The corrections are built with **field inversion (FI)** and **symbolic regression (SR)**, giving explicit algebraic corrections to the Spalart–Allmaras production term.
* **Low cost at runtime:** The model needs no additional transport equations and no neural-network inference.
* **Solver-independent:** The model was implemented in an independent flow solver and tested on canonical transition cases, a natural-laminar-flow transport wing, and a hovering rotor.

## ✅ Key Results
* Captures the main transition-front trends and the resulting changes in aerodynamic performance.
* For the hovering rotor, the model needed about **55% of the wall-clock time** of a comparable transport-equation transition model.

## 📄 Preprint
Seunghyun Joo, Younghyo Kim, Kwanjung Yee, "Mechanism-Separated Closed-Form Transition Modeling via Field Inversion and Symbolic Regression," arXiv:2609.24162 [physics.flu-dyn], 2026. [https://arxiv.org/abs/2609.24162](https://arxiv.org/abs/2609.24162)
