---
layout: page
title: Solvers
---

## &nbsp;
{: #Solvers }
### [_**hy2Foam**_](#hy2Foam)  
### [_**hyFoam**_](#hyFoam)  
### [_**hy2MhdFoam**_](#hy2MhdFoam)
### [_**dsmcFoam+**_](#dsmcFoam+)
### [_**pdFoam**_](#pdFoam)

<br>
  
--- 

###### &nbsp;
{: #hy2Foam }
<p align="center">
  <img src="/docs/img/logos/hy2FoamLogo.png" width="200"/>
</p>

_hy2Foam_ is an open-source two-temperature computational fluid dynamics (CFD)
solver that has been developed to tackle the highly complex flow physics of the hypersonic planetary
atmospheric entry. Implemented within the OpenFOAM framework, the code has the capability to model physical phenomena relative to the high-speed chemically-reacting environment surrounding a spacecraft. The core of the solver initially relied on OpenFOAM solvers _rhoCentralFoam_ and _reactingFoam_ and it has been complemented with many new features, some of which are listed below

* **non-equilibrium Navier-Stokes-Fourier equations**: **Park's two-temperature model** is implemented and the choice of having a single vibrational energy pool and multiple vibrational energy pools is left to the user. Energy transfers between the different energy pools are
  + Vibrational-Translational (V-T)
  + Vibrational-Vibrational (V-V)
  + Heavy particle-electron (H-e)
* addition of the electronic and electron energy modes
* finite-rate chemistry
* chemistry-vibration coupling: **Park TTv model**, coupled vibration-dissociation-vibration (CVDV) model
* customizable chemistry databases (Park 1993, Park 1994, Dunn & Kang 1973, quantum-kinetics: Scanlon 2015) including dissociation, electron impact dissociation, electron impact ionization, associative ionization, exchange and charge exchange reactions
* capability to handle species with several characteristic vibrational temperatures (_e.g._, CO2) for the Mars atmospheric entry
* transport models: Blottner and Eucken, power law and Eucken, Sutherland and Eucken, constant
* species diffusion models: Lewis number, generalised Fick's law, SCEBD model, inclusion of the effect of the pressure gradient
* mixing rules: Wilke, Armaly & Sutton
* turbulence models (no change made to OF-v1612+): laminar, k-omega SST, k-Epsilon, Spalart Allmaras, etc
* computation of the convective wall heat flux
* computation of the mean-free-path and the breakdown parameter
* boundary conditions: Smoluchowski temperature jump and Maxwell velocity slip BCs were adapted. Possibility to gradually increase the inlet flow velocity (rampInlet)  
* all dictionaries can be re-read on-the-fly: handy on a high-performance computer  
* layer functions for the strongly-coupled hybrid CFD-DSMC code _hyperFoam_  

[**> How-tos**](https://vincentcasseau.github.io/how-tos-cfd/)  
[**> Tutorials**](https://vincentcasseau.github.io/tutos-hy2foam/)  
[**> Source code**](https://github.com/vincentcasseau/hyStrath/tree/master/applications/solvers/compressible/hy2Foam)  
[**&#x2191; Back to Contents**](#Solvers)  

<br>
 
---  
###### &nbsp;
{: #hyFoam }
<p align="center"> 
  <img src="/docs/img/logos/hyFoamLogo.png" width="190"/>
</p>

_hyFoam_ is an open-source computational fluid dynamics (CFD)
solver that derives from _hy2Foam_. In the latter code, the trans-rotational and vibro-electronic energy modes are considered to be in thermal equilibrium, thus producing a single-temperature CFD solver. _hyFoam_ has the capability to model the high-speed chemically-reacting environment inside a scramjet. Most of _hy2Foam_ features remain accessible and _hyFoam_ further receives the addition of

* customizable chemistry databases (Evans & Schexnayder 1980, Jachimowski 1992)
* hydrogen compounds added to the thermochemical database
* transport models: CEA2 (Chemical Equilibrium with Applications, NASA)

[**> How-tos**](https://vincentcasseau.github.io/how-tos-cfd/)  
[**> Tutorials**](https://vincentcasseau.github.io/tutos-hyfoam/)  
[**> Source code**](https://github.com/vincentcasseau/hyStrath/tree/master/applications/solvers/compressible/hy2Foam)  
[**&#x2191; Back to Contents**](#Solvers)  

<br>

---  
  
###### &nbsp;
{: #hy2MhdFoam }
<p align="center">
  <img src="/docs/img/logos/hy2MhdFoamLogo.png" width="210"/>
</p>

By: A. Ryakhovskiy, Ioffe Institute & Peter the Great St. Petersburg Polytechnic University , St Petersburg, Russia  

_hy2MhdFoam_ supplements _hy2Foam_ with features relative to magnetohydrodynamics (MHD) flow control. The general objectives are to study the interaction between a high-speed ionized flow and the magnetic field, and to investigate the potential of MHD flow control technology on scramjet configurations.

* MHD terms added to the Navier-Stokes-Fourier equations
  + Lorentz force
  + Joule heating  
* Available electrical conductivity models
  + Boltzmann  
  + Spitzer-Harm  
  + Chapman-Cowling
  + Bush  
  + Raizer  
* Ongoing or planned developments
  + Hall effect  
  + Ion slip  
  + Artificial ionization  
  + P-1 radiation model  

[**> How-tos**](https://vincentcasseau.github.io/how-tos-cfd/)  
[**> Tutorials**](https://vincentcasseau.github.io/tutos-hy2mhdfoam/)  
[**> Source code**](https://github.com/vincentcasseau/hyStrath/tree/master/applications/solvers/compressible/hy2MhdFoam)  
[**&#x2191; Back to Contents**](#Solvers)  

<br>

---  
  
###### &nbsp;
{: #dsmcFoam+ }
<p align="center">
  <img src="/docs/img/logos/dsmcFoamPlusLogo.png" width="220"/>
</p>

A modified version of the _dsmcFoam+_ direct simulation Monte Carlo solver located at [MicroNanoFlows/OpenFOAM-2.4.0-MNF/tree/devel-craig](https://github.com/MicroNanoFlows/OpenFOAM-2.4.0-MNF/tree/devel-craig). The new features are the following

* improved load balancing feature
* improved axially-symmetric capability
* several variants for vibrational energy redistribution including a constant vibrational collision number
* corrections made to the calculation of macroscopic properties
* re-arranged wall boundary conditions and addition of the absorption & adsorption/desorption mechanisms
* measurement of the mean squared displacement (thus effective diffusivity) and particle transit time for porous media computations
* complete re-arrangement of the QK reaction classes
* extension of the QK reaction classes to Martian entry problems
* added capability to run steady normal shock wave computations
* layer functions for the strongly-coupled hybrid CFD-DSMC code _hyperFoam_
* Ongoing developments
  + adaptive mesh refinement (AMR)  
  + variable time-step method
  + extension of the QK reaction classes to Martian entry problems  

[**> How-tos**](https://vincentcasseau.github.io/how-tos-dsmc/)  
[**> Tutorials**](https://vincentcasseau.github.io/tutos-dsmcfoam/)  
[**> Source code**](https://github.com/vincentcasseau/hyStrath/tree/master/applications/solvers/discreteMethods/dsmc/dsmcFoam%2B)  
[**&#x2191; Back to Contents**](#Solvers)

<br>

---  
  
###### &nbsp;
{: #pdFoam }
<p align="center">
  <img src="/docs/img/logos/pdFoamLogo.png" width="190"/>
</p>

By: C. Capon, UNSW, Canberra, Australia  

[**> Tutorials**](https://vincentcasseau.github.io/tutos-pdfoam/)  
[**> Source code**](https://github.com/vincentcasseau/hyStrath/tree/master/applications/solvers/hybridMethods/pdFoam)  
[**&#x2191; Back to Contents**](#Solvers)
