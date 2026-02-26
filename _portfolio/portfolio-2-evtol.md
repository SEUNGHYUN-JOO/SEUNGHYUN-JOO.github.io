---
title: "eVTOL Downwash/Outwash Analysis using LBM"
excerpt: "Comprehensive aerodynamic characterization of various eVTOL configurations and validation of the Lattice-Boltzmann Method (LBM) for near-ground operations."
collection: portfolio
---

## 🔍 Project Overview
Investigated the complex aerodynamic interference of eVTOL aircraft during hover and near-ground operations to address the limitations of current heliport/vertiport safety regulations.

While current vertiport design standards define a fixed safety area (e.g., 2.5D), recent studies and surveys indicate that these criteria may not sufficiently account for configuration-dependent outwash hazards of multi-rotor eVTOL aircraft. 

This research aims to provide a high-fidelity aerodynamic assessment framework to support future regulation evolution.

## ⚙️ Methodology

### Lattice-Boltzmann Method (LBM)
Used SIMULIA PowerFLOW, a commercial LBM-based CFD solver featuring:

- Algebraic governing equations with lattice-level parallelization
- Low numerical dissipation for vortex-dominant rotor flows
- Efficient handling of moving geometries (rotors) via facet-based boundary treatment

LBM was selected to balance:
- High-fidelity unsteady rotor wake prediction
- Affordable computational cost for O(10²–10³) rotor revolutions
- Capability to model complex fuselage and ground geometries

### Solver Validation

Validation was performed at two levels:

1. **Aerodynamic Performance Validation**
   - ONERA M6 wing
   - ROBIN fuselage
   - Caradonna-Tung rotor
   → Good Cp distribution agreement with experiments.

2. **Downwash/Outwash Validation**
   - CH-47D tandem rotor helicopter
   - Compared against experimental survey data and RANS / RANS-ALM
   → Accurate prediction of outwash velocity profiles at 1 m AGL

### Configuration-Level Physical Insights

- **QSMR**: Tailboom–wake interaction produced a tail-shaped outwash hazard region.
- **Side-by-Side**: Strong rotor–rotor interaction generated directional front-to-back outwash jets.
- **Quadrotor**: High rotor height and low disk loading prevented any region from exceeding the 15 m/s hazard threshold.
- **Lift+Cruise (LPC)**: Extremely high disk loading led to hazard areas exceeding current safety regulation limits.

### External Wind Effects (Lift+Cruise Case)

- 5 m/s wind expanded hazard areas by up to 30%.
- 10 m/s forward wind increased the hazard radius to 63.6 m,
  approximately **3× the current safety area regulation**.
- Hazard expansion followed the order:
  Forward > Diagonal > Side wind.

These results indicate that even moderate wind conditions
far below the 25 m/s operational limit
can critically amplify ground-level outwash hazards.

## 🧭 Research Implications

This study highlights several open regulatory and technical questions:

- How should diverse eVTOL configurations be treated consistently in safety assessment?
- Which representative velocity metric should be used?
  (Time-averaged, RMS, 95th percentile, or absolute maximum?)
- Can existing military-based hazard models be applied to civilian UAM operations?

The findings suggest that current vertiport regulations may require configuration-aware and wind-sensitive updates.

## 🛠️ Key Technical Contributions

- Established a validated LBM-based workflow for rotorcraft downwash/outwash prediction.
- Demonstrated configuration-dependent hazard footprint variation across NASA UAM reference vehicles.
- Quantified wind-induced amplification of ground-level outwash, showing up to 3× safety-area exceedance.
- Provided physics-based insights into the influence of disk loading, rotor height, and rotor–rotor interaction.

## 👤 My Contributions

Although this work was conducted as a collaborative research project, my primary technical contributions focused on high-fidelity LBM validation and rotorcraft outwash prediction.

- Performed **Lattice-Boltzmann solver validation** against canonical aerodynamic benchmark cases (ONERA M6, ROBIN fuselage, Caradonna-Tung rotor).
- Conducted **CH-47D tandem rotor downwash/outwash validation**:
  - Simulated 150 rotor revolutions with final 50-rev time averaging.
  - Compared ground-level velocity profiles with experimental survey data and RANS/RANS-ALM results.
- Executed **Joby S4 eVTOL geometry-based validation simulations**, verifying wake structure and near-ground velocity distribution behavior.
- Analyzed velocity-field data to assess hazard threshold exceedance (15 m/s DCA criterion).

My role centered on establishing solver credibility and ensuring the physical reliability of the downwash/outwash prediction framework.

## 📚 Publications
* **Juneyoung Lim, Seunghyun Joo, Kwanjung Yee.** (2025). "Downwash/Outwash Analysis of eVTOL Configurations Using the Lattice-Boltzmann Method," *APISAT 2025*.


<div style="max-width: 1000px; margin: 40px auto;">
  <img src="{{ '/assets/images/portfolio-2-evtol/슬라이드1.PNG' | relative_url }}" 
       style="width:100%; height:auto; display:block; margin-bottom:40px;">
  <img src="{{ '/assets/images/portfolio-2-evtol/슬라이드7.PNG' | relative_url }}" 
       style="width:100%; height:auto; display:block; margin-bottom:40px;">
  <img src="{{ '/assets/images/portfolio-2-evtol/슬라이드10.PNG' | relative_url }}" 
       style="width:100%; height:auto; display:block; margin-bottom:40px;">
  <img src="{{ '/assets/images/portfolio-2-evtol/슬라이드11.PNG' | relative_url }}" 
       style="width:100%; height:auto; display:block; margin-bottom:40px;">
  <img src="{{ '/assets/images/portfolio-2-evtol/슬라이드13.PNG' | relative_url }}" 
       style="width:100%; height:auto; display:block; margin-bottom:40px;">
  <img src="{{ '/assets/images/portfolio-2-evtol/슬라이드16.PNG' | relative_url }}" 
       style="width:100%; height:auto; display:block; margin-bottom:40px;">
  <img src="{{ '/assets/images/portfolio-2-evtol/슬라이드18.PNG' | relative_url }}" 
       style="width:100%; height:auto; display:block; margin-bottom:40px;">
  <img src="{{ '/assets/images/portfolio-2-evtol/슬라이드20.PNG' | relative_url }}" 
       style="width:100%; height:auto; display:block; margin-bottom:40px;">
  <img src="{{ '/assets/images/portfolio-2-evtol/슬라이드22.PNG' | relative_url }}" 
       style="width:100%; height:auto;">
</div>
<div style="max-width: 900px; margin: auto;">
  <video style="width: 100%; height: auto;" controls>
    <source src="{{ '/assets/videos/portfolio-2-evtol/CH-47D.mp4' | relative_url }}" type="video/mp4">
  </video>
</div>