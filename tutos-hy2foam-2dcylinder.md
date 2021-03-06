---
layout: page
title: Tutorials
nav-short: true
---
  
<p align="center">
  <img src="/docs/img/logos/hy2FoamLogo.png" width="210">
</p>

# 2D Cylinder

+ The working directory for the 2D planar cylinder is located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/cylinderReactingMach20). 

+ A description of the case scenario can be found in: V. Casseau _et al._, 12/2016: [A Two-Temperature Open-Source CFD Model for Hypersonic Reacting Flows, Part Two: Multi-Dimensional Analysis](http://www.mdpi.com/2226-4310/3/4/45/html), Section _3.2. Mach 20 Cylinder_. 

+ Running this tutorial:  
This tutorial is given in the form of a very high-speed flow simulation exercise. When simulating the complex physics around a re-entry body, it is often necessary to break down the full problem into a sequence of stages and gradually build the case up in complexity. Indeed, convergence can become difficult because of the presence of steep gradients, flow chemistry, thermal non-equilibrium effects, etc, and different strategies must then be adopted to get the desired simulation setup to run.  
Some of these strategies are listed hereafter:  
  1- different levels of mesh refinement as the simulation progresses;  
  2- [non-reacting vs. reacting](https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordia-chemistry/#2-non-reacting-flow);  
  3- [continuum vs. rarefied boundary conditions](https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordia-initial-conditions/#3-temperature-fields);   
  4- [bounding the temperature field](https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordia-advanced/#3-bounding-the-temperature-field);  
  5- [Mach ramp](https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordia-initial-conditions/#42-linear-inlet-ramp) at the inlet;  
  6- [inviscid vs. viscous flow](https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordia-transport/#transport-modelling);  
  7- [no diffusion vs. species diffusion](https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordia-transport/#3-mass-diffusion);  
  8- use of the [continuum solver *hyFoam* vs. thermal non-equilibrium solver *hy2Foam*](https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordia-nonequilibrium/#1-thermal-equilibrium)  
  9- progressive increase in the [degree of rarefaction](https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordia-nonequilibrium/#32-knudsen-number);  
  10- gradual increase in the maximum CFL number;   
  11- etc.

In the present case, special attention is drawn to points 1, 2, 3, 4, 5 and 7.

**NB: The setup provided in the [working directory](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/cylinderReactingMach20) corresponds to the last stage of the simulation.**
  
After deciding what your stages will be and setting up the different working folders accordingly, you can sequentially run    
```sh
./Allclean  
./Allrun
```   
and map results from one stage to the next using the *mapFields -consistent* utility and the latest printed time folder of the current stage.

<br>

+ Solution: CFD-DSMC flow-field comparisons

<p align="center">
  <img src="http://www.mdpi.com/aerospace/aerospace-03-00045/article_deploy/html/images/aerospace-03-00045-g004.png" width="800">
</p>

> _Computational fluid dynamics-direct simulation Monte Carlo (CFD-DSMC) flow-field comparisons for run number 2. In (b–d): the dsmcFoam solution is represented in the upper half and the hy2Foam solution in the lower half. (a) Local gradient-length Knudsen number; (b) Mach number; (c) trans-rotational temperature; and (d) vibrational temperature._ 

<br>

+ Erratum: there is a typo with the integrated convective wall heat fluxes that should be multiplied by a factor of 2 in Table 5: _Aerothermodynamic coefficients_.

+ NB: the simulations shown in this journal article were obtained using a version of _hy2Foam_ dated May 2016. Multi-species diffusion modelling has been improved and the available options now differ. Thus, inconsistencies might exist in the aerothermodynamic coefficients.

<br>

---  

Contributor: Dr Vincent Casseau
