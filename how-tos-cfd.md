---
layout: page
title: How-tos
subtitle: CFD Module
---

These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/genericCase).  

# Table of contents

---  
## [A. How-to :: Thermophysical](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Thermophysical)
### [1) Species thermophysical properties](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Thermophysical#1-species-thermophysical-properties)
+ **[1.1 Disabling/enabling the vibrational mode of a molecule](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#11-disablingenabling-the-vibrational-mode-of-a-molecule)**  
+ **[1.2 Disabling/enabling the electronic mode of a particle](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#12-disablingenabling-the-electronic-mode-of-a-particle)**  

<br>

---  
## [B. How-to :: Transport](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport)
### [1) Species thermophysical properties](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#1-individual-shear-viscosity-and-thermal-conductivity)
+ **[1.1 Inviscid simulation](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#11-inviscid-simulation)**  
+ **[1.2 Viscous simulation with constant shear viscosity and thermal conductivity](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#12-viscous-simulation-with-constant-shear-viscosity-and-thermal-conductivity)**  
+ **[1.3 Other transport models](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#13-to-go-further)**  
+ **[1.4 Print species shear viscosity and thermal conductivity](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#14-print-species-shear-viscosity-and-thermal-conductivity)**  

### [2) Mixing rules](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#2-mixing-rules)  

### [3) Mass diffusion](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#3-mass-diffusion)  
+ **[3.1 Disable multi-species diffusion](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#31-disable-multi-species-diffusion)**  
+ **[3.2 Lewis number model](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#32-lewis-number-model)**  
+ **[3.3 Fick's law and binary diffusion models](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#33-ficks-law-and-binary-diffusion-models)**  
+ **[3.4 SCEBD model](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#34-scebd-model)**  
+ **[3.5 Additional features (to Fick and SCEBD models)](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#35-additional-features-to-fick-and-scebd-models)**  

<br>

---  
## [C. How-to :: Chemistry](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry)
### [1) Multi-species flow](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#1-multi-species-flow)
+ **[1.1 The _chemDicts/_ folder](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#11-the-chemdicts-folder)**  
+ **[1.2 Adding/deleting species](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#12-addingdeleting-species)** 
+ **[1.3 Printing species quantities](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#13-printing-species-quantities)**  

### [2) Non-reacting flow](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#2-non-reacting-flow)

### [3) Chemically-reacting flow](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#3-chemically-reacting-flow)
+ **[3.1 Enable chemistry](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#31-enable-chemistry)**  
+ **[3.2 Implement a chemical reaction](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#32-implementing-a-chemical-reaction)**  
      - [3.2.1 Forward reaction](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#321-forward-reaction)  
      - [3.2.2 Reverse reaction](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#322-reverse-reaction)  
      - [3.2.3 Third-body interaction](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#323-third-body-interaction)  
+ **[3.3 Increase robustness](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#33--increase-robustness)**  

### [4) To go further: chemistry-vibration coupling](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#4-to-go-further-chemistry-vibration-coupling)

<br>

--- 
## [D. How-to :: Nonequilibrium](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium)
### [1) Thermal equilibrium](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#1-thermal-equilibrium)

### [2) Thermal non-equilibrium](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#2-thermal-non-equilibrium)
+ **[2.1 Two-temperature solver, single vibro-electronic energy pool](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#21-two-temperature-solver-single-vibro-electronic-energy-pool)**  
+ **[2.2 Two-temperature solver, multiple vibro-electronic energy pools](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#22-two-temperature-solver-multiple-vibro-electronic-energy-pools)** 

### [3) Mean free path and breakdown parameter](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#3-mean-free-path-and-breakdown-parameter)  
+ **[3.1 Mean free path](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#31-mean-free-path)**    
+ **[3.2 Knudsen number](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#32-knudsen-number)**  
      - [3.2.1 Overall Knudsen number](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#321-overall-knudsen-number)  
      - [3.2.2 Breakdown parameter: gradient-length Knudsen number](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#322-breakdown-parameter-gradient-length-knudsen-number)  

### [4) Chemistry-vibration coupling](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#4-chemistry-vibration-coupling)  
+ **[4.1 Park TTv model](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#41-park-ttv-model)**  
      - [4.1.1 General settings](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#411-general-settings)  
      - [4.1.2 Reactions dictionary](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#412-reactions-dictionary)  
+ **[4.2 Coupled vibration-dissociation-vibration (CVDV) model](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#42-coupled-vibration-dissociation-vibration-cvdv-model)**       

<br>

---  
## [E. How-to :: Turbulence](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Turbulence)
### [1) Laminar flow simulation](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Turbulence#1-laminar-flow-simulation) 
 
### [2) Turbulent flow simulation](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Turbulence#2-turbulent-flow-simulation) 

<br>

---  
## F. How-to :: MHD

<br>

---  
## [G. How-to :: Initial conditions](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions)

### [1) The _include/_ sub-folder](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions#1-the-include-sub-folder)

### [2) Species mass fractions](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions#2-species-mass-fractions)  
+ **[2.1 Non-catalytic wall](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions#21-non-catalytic-wall)**  
+ **[2.2 Super-catalytic wall](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions#22-super-catalytic-wall)**

### [3) Temperature fields](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions#3-temperature-fields)  
+ **[3.1 Trans-rotational temperature](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions#31-trans-rotational-temperature)**  
+ **[3.2 Vibro-electronic temperature](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions#32-vibro-electronic-temperature)**  
      - [3.2.1 Single vibro-electronic energy pool formulation](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions#321-single-vibro-electronic-energy-pool-formulation)  
      - [3.2.2 Multiple vibro-electronic energy pools formulation](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions#322-multiple-vibro-electronic-energy-pools-formulation)   
 
### [4) Velocity field](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions#4-velocity-field)  

<br>

---  
## [H. How-to :: Advanced](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Advanced)

### [1) Local time stepping](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Advanced#1-local-time-stepping)  

### [2) On-the-fly dictionary editing](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Advanced#2-on-the-fly-dictionary-editing)  

### [3) Bounding the temperature field](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Advanced#3-bounding-the-temperature-field) 

### [4) The _hyLight_ switch](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Advanced#4-the-hylight-switch)   

<br>

---  
## [I. How-to :: Monitoring & Post-processing](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Monitoring-&-Post-processing)

### [1) Monitoring](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Monitoring-&-Post-processing#1-monitoring)  
+ **[1.1 Wall heat flux](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Monitoring-&-Post-processing#11-wall-heat-flux)**  
+ **[1.2 Wall shear stress](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Monitoring-&-Post-processing#12-wall-shear-stress)**
+ **[1.3 Forces](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Monitoring-&-Post-processing#13-forces)**  
+ **[1.4 Residuals](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Monitoring-&-Post-processing#14-residuals)**  

### [2) Post-processing](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Monitoring-&-Post-processing#2-post-processing)  
+ **[2.1 Pressure coefficient](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Monitoring-&-Post-processing#21-pressure-coefficient)**  
+ **[2.2 Stanton number](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Monitoring-&-Post-processing#22-stanton-number)**  
+ **[2.3 Skin-friction coefficient](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Monitoring-&-Post-processing#23-skin-friction-coefficient)**  
+ **[2.4 _y+_](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Monitoring-&-Post-processing#24-y)**  
+ **[2.5 ParaView](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Monitoring-&-Post-processing#25-paraview)**  
