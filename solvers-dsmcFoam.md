---
layout: page
title: Solvers
---

## &nbsp;
{: #Solvers }
### [_**hy2Foam**_](https://vincentcasseau.github.io/solvers-hy2Foam/)  
### [_**hyFoam**_](#https://vincentcasseau.github.io/solvers-hyFoam/)  
### [_**hy2MhdFoam**_](#https://vincentcasseau.github.io/solvers-hy2MhdFoam/)
### [_**dsmcFoam+**_](#https://vincentcasseau.github.io/solvers-dsmcFoam/)
### [_**pdFoam**_](#https://vincentcasseau.github.io/solvers-pdFoam/)

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
