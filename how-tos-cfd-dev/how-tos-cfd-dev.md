---
layout: page
title: How-tos
subtitle: CFD Module, next Release
nav-short: true
---

These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/genericCase).  

# Table of contents

---  
## [A. Thermophysical](https://vincentcasseau.github.io/how-tos-cfd-dev-thermophysical/)
### [1) Species thermophysical properties](https://vincentcasseau.github.io/how-tos-cfd-dev-thermophysical/#1-species-thermophysical-properties)
### [2) Adding/removing energy modes](https://vincentcasseau.github.io/how-tos-cfd-dev-thermophysical/#2-addingremoving-energy-modes)
+ **[2.1 Disabling/enabling the vibrational mode of a molecule](https://vincentcasseau.github.io/how-tos-cfd-dev-thermophysical/#21-disablingenabling-the-vibrational-mode-of-a-molecule)**  
+ **[2.2 Disabling/enabling the electronic mode of a particle](https://vincentcasseau.github.io/how-tos-cfd-dev-thermophysical/#22-disablingenabling-the-electronic-mode-of-a-particle)**  

<br>

---  
## [B. Transport](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/)
### [1) Species transport properties](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/#1-species-shear-viscosity-and-thermal-conductivity)
+ **[1.1 Inviscid simulation](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/#11-inviscid-simulation)**  
+ **[1.2 Viscous simulation with constant shear viscosity and thermal conductivity](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/#12-viscous-simulation-with-constant-shear-viscosity-and-thermal-conductivity)**  
+ **[1.3 Other transport models](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/#13-other-transport-models)**  
+ **[1.4 Print species shear viscosity and thermal conductivity](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/#14-print-species-shear-viscosity-and-thermal-conductivity)**  

### [2) Mixing rules](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/#2-mixing-rules)  

### [3) Mass diffusion](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/#3-mass-diffusion)  
+ **[3.1 Disable multi-species diffusion](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/#31-disable-multi-species-diffusion)**  
+ **[3.2 Lewis number model](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/#32-lewis-number-model)**  
+ **[3.3 Fick's law and binary diffusion models](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/#33-ficks-law-and-binary-diffusion-models)**  
+ **[3.4 SCEBD model](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/#34-scebd-model)**  
+ **[3.5 Additional features (to Fick and SCEBD models)](https://vincentcasseau.github.io/how-tos-cfd-dev-transport/#35-additional-features-to-fick-and-scebd-models)**  

<br>

---  
## [C. Chemistry](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/)
### [1) Multi-species flow](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#1-multi-species-flow)
+ **[1.1 The _chemDicts/_ folder](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#11-the-chemdicts-folder)**  
+ **[1.2 Adding/deleting species](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#12-addingdeleting-species)** 
+ **[1.3 Printing species quantities](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#13-printing-species-quantities)**  

### [2) Non-reacting flow](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#2-non-reacting-flow)

### [3) Chemically-reacting flow](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#3-chemically-reacting-flow)
+ **[3.1 Enable chemistry](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#31-enable-chemistry)**  
+ **[3.2 Implement a chemical reaction](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#32-implementing-a-chemical-reaction)**  
      - [3.2.1 Forward reaction](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#321-forward-reaction)  
      - [3.2.2 Reverse reaction](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#322-reverse-reaction)  
      - [3.2.3 Third-body interaction](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#323-third-body-interaction)  
+ **[3.3 Increase robustness](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#33--increase-robustness)**  

### [4) To go further: chemistry-vibration coupling](https://vincentcasseau.github.io/how-tos-cfd-dev-chemistry/#4-to-go-further-chemistry-vibration-coupling)

<br>

--- 
## [D. Nonequilibrium](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/)
### [1) Thermal equilibrium](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#1-thermal-equilibrium)

### [2) Thermal non-equilibrium](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#2-thermal-non-equilibrium)
+ **[2.1 Single vibro-electronic energy pool](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#21-single-vibro-electronic-energy-pool)**  
+ **[2.2 Multiple vibro-electronic energy pools](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#22-multiple-vibro-electronic-energy-pools)** 

### [3) Mean free path and breakdown parameter](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#3-mean-free-path-and-breakdown-parameter)  
+ **[3.1 Mean free path](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#31-mean-free-path)**    
+ **[3.2 Knudsen number](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#32-knudsen-number)**  
      - [3.2.1 Overall Knudsen number](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#321-overall-knudsen-number)  
      - [3.2.2 Breakdown parameter: gradient-length Knudsen number](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#322-breakdown-parameter-gradient-length-knudsen-number)  

### [4) Chemistry-vibration coupling](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#4-chemistry-vibration-coupling)  
+ **[4.1 Park TTv model](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#41-park-ttv-model)**  
      - [4.1.1 General settings](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#411-general-settings)  
      - [4.1.2 Reactions dictionary](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#412-reactions-dictionary)  
+ **[4.2 Coupled vibration-dissociation-vibration (CVDV) model](https://vincentcasseau.github.io/how-tos-cfd-dev-nonequilibrium/#42-coupled-vibration-dissociation-vibration-cvdv-model)**       

<br>

---  
## [E. Turbulence](https://vincentcasseau.github.io/how-tos-cfd-dev-turbulence/)
### [1) Laminar flow simulation](https://vincentcasseau.github.io/how-tos-cfd-dev-turbulence/#1-laminar-flow-simulation) 
 
### [2) Turbulent flow simulation](https://vincentcasseau.github.io/how-tos-cfd-dev-turbulence/#2-turbulent-flow-simulation) 

<br>

---  
## [F. MHD](https://vincentcasseau.github.io/how-tos-cfd-dev-mhd/)

<br>

---  
## [G. Initial conditions](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/)

### [1) The _include/_ sub-folder](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/#1-the-include-sub-folder)

### [2) Species mass fractions](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/#2-species-mass-fractions)  
+ **[2.1 Non-catalytic wall](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/#21-non-catalytic-wall)**  
+ **[2.2 Super-catalytic wall](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/#22-super-catalytic-wall)**

### [3) Temperature fields](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/#3-temperature-fields)  
+ **[3.1 Trans-rotational temperature](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/#31-trans-rotational-temperature)**  
+ **[3.2 Vibro-electronic temperature](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/#32-vibro-electronic-temperature)**  
      - [3.2.1 Single vibro-electronic energy pool formulation](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/#321-single-vibro-electronic-energy-pool-formulation)  
      - [3.2.2 Multiple vibro-electronic energy pools formulation](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/#322-multiple-vibro-electronic-energy-pools-formulation)   
 
### [4) Velocity field](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/#4-velocity-field)  
+ **[4.1 Maxwell velocity slip](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/#41-maxwell-velocity-slip)**  
+ **[4.2 Linear inlet ramp](https://vincentcasseau.github.io/how-tos-cfd-dev-initial-conditions/#42-linear-inlet-ramp)**  

<br>

---  
## [H. Advanced](https://vincentcasseau.github.io/how-tos-cfd-dev-advanced/)

### [1) Local time stepping](https://vincentcasseau.github.io/how-tos-cfd-dev-advanced/#1-local-time-stepping)  

### [2) On-the-fly dictionary editing](https://vincentcasseau.github.io/how-tos-cfd-dev-advanced/#2-on-the-fly-dictionary-editing)  

### [3) Bounding the temperature field](https://vincentcasseau.github.io/how-tos-cfd-dev-advanced/#3-bounding-the-temperature-field) 

### [4) The _hyLight_ switch](https://vincentcasseau.github.io/how-tos-cfd-dev-advanced/#4-the-hylight-switch)   

### [5) Adaptive mesh refinement](https://vincentcasseau.github.io/how-tos-cfd-dev-advanced/#5-adaptive-mesh-refinement)  

<br>

---  
## [I. Monitoring & Post-processing](https://vincentcasseau.github.io/how-tos-cfd-dev-monitoring-post-processing)

### [1) Monitoring](https://vincentcasseau.github.io/how-tos-cfd-dev-monitoring-post-processing/#1-monitoring)  
+ **[1.1 Wall heat flux](https://vincentcasseau.github.io/how-tos-cfd-dev-monitoring-post-processing/#11-wall-heat-flux)**  
+ **[1.2 Wall shear stress](https://vincentcasseau.github.io/how-tos-cfd-dev-monitoring-post-processing/#12-wall-shear-stress)**
+ **[1.3 Forces](https://vincentcasseau.github.io/how-tos-cfd-dev-monitoring-post-processing/#13-forces)**  
+ **[1.4 Residuals](https://vincentcasseau.github.io/how-tos-cfd-dev-monitoring-post-processing/#14-residuals)**  

### [2) Post-processing](https://vincentcasseau.github.io/how-tos-cfd-dev-monitoring-post-processing/#2-post-processing)  
+ **[2.1 Pressure coefficient](https://vincentcasseau.github.io/how-tos-cfd-dev-monitoring-post-processing/#21-pressure-coefficient)**  
+ **[2.2 Stanton number](https://vincentcasseau.github.io/how-tos-cfd-dev-monitoring-post-processing/#22-stanton-number)**  
+ **[2.3 Skin-friction coefficient](https://vincentcasseau.github.io/how-tos-cfd-dev-monitoring-post-processing/#23-skin-friction-coefficient)**  
+ **[2.4 _y+_](https://vincentcasseau.github.io/how-tos-cfd-dev-monitoring-post-processing/#24-y)**  
+ **[2.5 ParaView](https://vincentcasseau.github.io/how-tos-cfd-dev-monitoring-post-processing/#25-paraview)**  
