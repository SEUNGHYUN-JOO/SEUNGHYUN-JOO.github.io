---
title: "AMADEVS: A Generalized Aircraft Modeling & Analysis Environment for Multidisciplinary Design"
collection: publications
category: conferences
permalink: /publication/2026-amadevs
date: 2026-01-01
venue: 'AIAA SCITECH 2026 Forum'
paperurl: 'https://doi.org/10.2514/6.2026-1687'
excerpt: 'A generalized aircraft modeling and analysis environment with role-based components and a dual geometry–energy topology, demonstrated on Mars helicopter sizing, wing design under propeller–wing interaction, and UAM quadcopter handling qualities.'
citation: 'Jeonghwan Kim, Seongjoong Park, Berenice Chatelain, Seonghyun Jeong, Jaehyun Ryu, **Seunghyun Joo**, and Kwanjung Yee. (2026). "AMADEVS: A Generalized Aircraft Modeling & Analysis Environment for Multidisciplinary Design." *AIAA SCITECH 2026 Forum*, 1687.'
---

[![DOI](https://img.shields.io/badge/DOI-10.2514%2F6.2026--1687-blue)](https://doi.org/10.2514/6.2026-1687)

## 🔍 Overview
**AMADEVS** (Advanced Modeling, Analysis & Design Environment for Vehicle Systems) is a generalized aircraft analysis and design environment developed at AVDL, Seoul National University. It is built for the growing variety of aircraft configurations (multi-rotor eVTOLs, tailsitters, tiltrotors, strut-braced wings) and propulsion architectures (electric, fuel-cell, hybrid, and distributed propulsion).

* **Role-based components:** every component is defined by its role in the system (lift generation, thrust generation, power conversion, energy storage).
* **Dual topology:** the physical assembly (geometry topology) and the energy and signal flows (energy topology) are modeled as coupled graphs.
* **One model for all disciplines:** aerodynamic, propulsion, flight-dynamics & control, and mission analyses run on the same aircraft model, with selectable fidelity for each component.
* **Framework builder:** AMADEVS also serves as a base for other design frameworks, such as RISPECT III (rotorcraft) and ASPECT (fixed-wing).

<figure>
  <img src="{{ '/assets/images/portfolio-3-amadevs/amadevs_architecture.png' | relative_url }}" alt="AMADEVS architecture overview">
  <figcaption>AMADEVS architecture overview: object-based component definition, topology-based system assembly, and multidisciplinary analysis integration.</figcaption>
</figure>

The paper presents three application studies: sizing of a Mars helicopter, **wing design under propeller–wing interaction**, and handling-qualities analysis of a UAM quadcopter.

---

## 🛠️ My Contribution: Wing Design Optimization Under Propeller–Wing Interaction
I carried out the **propeller–wing interaction (PWI)** case study, which shows how AMADEVS handles coupling between components (the propeller slipstream acting on the wing) inside a multidisciplinary optimization.

* **Aero-propulsive coupling:** an in-house vortex lattice method (VLM) for the wing, coupled with a QPROP-type blade element model for the propeller. The propeller-induced velocity field is added at each VLM control point instead of treating the slipstream as a uniform inflow.
* **Validation:** the coupled solver was compared with the PROWIM wind-tunnel experiment. It captures the asymmetric lift distortion caused by propeller swirl (upwash on the up-going blade side, downwash on the down-going blade side).
* **Bi-objective MDO:** cruise power versus wing-box structural weight for an X-57 Mod 2-like configuration, with nine design variables (aspect ratio, taper ratio, segmented twist, and propeller location, radius, blade count, and rotation direction), solved with NSGA-II.

<figure>
  <img src="{{ '/assets/images/portfolio-3-amadevs/pwi_prowim_validation.png' | relative_url }}" alt="PROWIM validation of the coupled VLM-propeller solver" style="max-width:640px; display:block; margin:auto;">
  <figcaption>Validation against the PROWIM experiment: spanwise lift distributions with the propeller off and on (inboard-up and outboard-up rotation).</figcaption>
</figure>

<figure>
  <img src="{{ '/assets/images/portfolio-3-amadevs/pwi_pareto_front.png' | relative_url }}" alt="Pareto front of cruise power versus wing box weight" style="max-width:720px; display:block; margin:auto;">
  <figcaption>Pareto front between cruise power and wing-box weight, with the minimum-power (A), balanced (B), and minimum-weight (C) designs.</figcaption>
</figure>

<figure>
  <img src="{{ '/assets/images/portfolio-3-amadevs/pwi_optimal_designs.png' | relative_url }}" alt="Wing planform, twist, lift and drag distributions of the selected designs" style="max-width:720px; display:block; margin:auto;">
  <figcaption>Planform, twist, lift, and drag distributions of the selected designs. The optimizer places a sharp change in twist at the propeller station: higher incidence in the inboard upwash region and strong washout in the outboard downwash region.</figcaption>
</figure>

### Key findings
* The minimum-power designs favor high aspect ratios (AR ≈ 11.7) but need a heavier wing box; the minimum-weight designs use lower aspect ratios and shift the lift inboard.
* The inboard section, which sees the upwash of the up-going blade, is loaded more so that its lift vector tilts forward and offsets drag. The outboard section is washed out, which also lowers the root bending moment.
* The best propeller location depends on how energy efficiency is weighed against structural weight, so the wing and propeller should be designed as one system.
