---
layout: page
title: Tutorials
nav-short: true
---

<p align="center">
  <img src="/docs/img/logos/hy2FoamLogo.png" width="210">
</p>


---  

# 1) Adiabatic heat bath

<p align="center">
Vibrational excitation | Thermal non-equilibrium | Chemistry-vibration coupling  
</p>

+ The working directory for the heat bath case is located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/heatBath).  

+ A description can be found in: V. Casseau _et al._, 10/2016: [A Two-Temperature Open-Source CFD Model for Hypersonic Reacting Flows, Part One: Zero-Dimensional Analysis](http://www.mdpi.com/2226-4310/3/4/34/html), Section _3.4. Relaxation of a Chemically-Reacting Mixture_.  

+ [View more](https://vincentcasseau.github.io/tutos-hy2foam-heatbath/)

<br>

---  

# 2) Blunted cone

<p align="center">
Axially-symmetric flow-field | Thermal non-equilibrium | Slip boundary conditions  
</p>

+ The working directory for the 2D axisymmetric blunted cone is located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/bluntedCone).  

+ A description can be found in: V. Casseau _et al._, 12/2016: [A Two-Temperature Open-Source CFD Model for Hypersonic Reacting Flows, Part Two: Multi-Dimensional Analysis](http://www.mdpi.com/2226-4310/3/4/45/html), Section _3.1. Mach 11.3 Blunted Cone_.  

+ [View more](https://vincentcasseau.github.io/tutos-hy2foam-bluntedcone/)


<br>

--- 

# 3) Running your own case 

When simulating the complex physics around a re-entry body, it is often necessary to break down the full problem into a sequence of stages and gradually build the case up in complexity. Indeed, convergence can become difficult because of the presence of steep gradients, flow chemistry, thermal non-equilibrium effects, etc, and different strategies must then be adopted to get the desired simulation setup to run.  
Some of these strategies are listed hereafter:  
  1- different levels of mesh refinement as the simulation progresses;  
  2- [non-reacting vs. reacting](https://vincentcasseau.github.io/how-tos-cfd-fleming/how-tos-cfd-fleming-chemistry/#2-non-reacting-flow);  
  3- [continuum vs. rarefied boundary conditions](https://vincentcasseau.github.io/how-tos-cfd-fleming/how-tos-cfd-fleming-initial-conditions/#3-temperature-fields);   
  4- [bounding the temperature field](https://vincentcasseau.github.io/how-tos-cfd-fleming/how-tos-cfd-fleming-advanced/#3-bounding-the-temperature-field);  
  5- [Mach ramp](https://vincentcasseau.github.io/how-tos-cfd-fleming/how-tos-cfd-fleming-initial-conditions/#42-linear-inlet-ramp) at the inlet;  
  6- [inviscid vs. viscous flow](https://vincentcasseau.github.io/how-tos-cfd-fleming/how-tos-cfd-fleming-transport/#transport-modelling);  
  7- [no diffusion vs. species diffusion](https://vincentcasseau.github.io/how-tos-cfd-fleming/how-tos-cfd-fleming-transport/#3-mass-diffusion);  
  8- use of the [continuum solver *hyFoam* vs. thermal non-equilibrium solver *hy2Foam*](https://vincentcasseau.github.io/how-tos-cfd-fleming/how-tos-cfd-fleming-nonequilibrium/#1-thermal-equilibrium)  
  9- progressive increase in the [degree of rarefaction](https://vincentcasseau.github.io/how-tos-cfd-fleming/how-tos-cfd-fleming-nonequilibrium/#32-knudsen-number);  
  10- gradual increase in the maximum CFL number.
  
<!--<br>-->

<!-----  -->

<!--# 3) 2D Cylinder-->

<!--<p align="center">-->
<!--Hypervelocity flow | Thermal non-equilibrium | Chemically reacting flow-->
<!--</p>-->

<!--+ The working directory for the 2D planar cylinder is located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/cylinderReactingMach20). -->

<!--+ A description can be found in: V. Casseau _et al._, 12/2016: [A Two-Temperature Open-Source CFD Model for Hypersonic Reacting Flows, Part Two: Multi-Dimensional Analysis](http://www.mdpi.com/2226-4310/3/4/45/html), Section _3.2. Mach 20 Cylinder_.  -->

<!--+ [View more](https://vincentcasseau.github.io/tutos-hy2foam-2dcylinder/)-->
