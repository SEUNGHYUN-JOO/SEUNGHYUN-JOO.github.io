---
permalink: /
title: "About Me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

# 👋 Hello, I'm Seunghyun Joo

I am a **Master's student** at the **Aerospace Vehicle Design Laboratory (AVDL)**, Seoul National University. My research lies at the intersection of **Fluid Dynamics** and **Data-Driven Science**, with a specific focus on **Turbulence Modeling** and **Physics-Informed Machine Learning**.

I am currently seeking a **Ph.D. position** for [Fall 2027] where I can contribute to the development of next-generation turbulence closures and flow control strategies using Artificial Intelligence.

---

## 🔍 Research Interests
My research goal is to develop robust aerodynamic models by integrating physics-based simulations with data-driven techniques.

* **Data Assimilation & AI:** Enhancing turbulence models and flow field reconstruction using machine learning and data assimilation techniques.
* **Multi-Fidelity Aerodynamic Analysis:** Expertise in Low (VLM, Panel method), Mid (LBM), and High-fidelity (RANS/LES/DNS) CFD simulations.

---

## 🎓 Education
* **M.S. in Aerospace Engineering**, Seoul National University, *Sep 2024 – Present*
* **B.S. in Aerospace Engineering & Business Administration (Double Major)**, Seoul National University, *Aug 2024*

---

## 📚 Publications
{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}

---

## 🛠️ Research Projects & Portfolio
{% for post in site.portfolio reversed %}
  {% include archive-single.html %}
{% endfor %}

---

## ✉️ Contact
* **Email:** [chlrh45351@gmail.com](mailto:chlrh45351@gmail.com)
