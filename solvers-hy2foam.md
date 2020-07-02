---
layout: page
title: Solvers
---

## &nbsp;
{: #Solvers }
### [_**hy2Foam**_](https://vincentcasseau.github.io/solvers-hy2foam/)  
### [_**hyFoam**_](https://vincentcasseau.github.io/solvers-hyfoam/)  
### [_**hy2MhdFoam**_](https://vincentcasseau.github.io/solvers-hy2mhdfoam/)
### [_**dsmcFoam+**_](https://vincentcasseau.github.io/solvers-dsmcfoam/)
### [_**pdFoam**_](https://vincentcasseau.github.io/solvers-pdfoam/)

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
[**> Disclaimer**](https://vincentcasseau.github.io/disclaimer/)  
[**&#x2191; Back to Contents**](#Solvers)
