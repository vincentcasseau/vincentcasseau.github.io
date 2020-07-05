---
layout: page
title: Solvers
nav-short: true
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
{: #dsmcFoam+ }
<p align="center">
  <img src="/docs/img/logos/dsmcFoamPlusLogo.png" width="220"/>
</p>

A modified version of the <i>dsmcFoam+</i> direct simulation Monte Carlo (DSMC) solver was added end of 2017 as part of a European Space Agency project. The original <i>dsmcFoam+</i> code is available at [MicroNanoFlows/OpenFOAM-2.4.0-MNF/tree/devel-craig](https://github.com/MicroNanoFlows/OpenFOAM-2.4.0-MNF/tree/devel-craig). The new features are as follows

* improved load balancing feature
* improved axially-symmetric capability
* inclusion of several variants for vibrational energy redistribution including a constant vibrational collision number
* corrections made to the calculation of macroscopic properties
* re-arranged wall boundary conditions and addition of the absorption & adsorption/desorption mechanisms
* measurement of the mean squared displacement (thus effective diffusivity) and particle transit time for porous media computations
* complete re-arrangement of the QK reaction classes
* added capability to run steady normal shock wave computations
* layer functions for the strongly-coupled hybrid CFD-DSMC code _hyperFoam_
* Ongoing developments
  + adaptive mesh refinement (AMR)  
  + variable time-step method
  + modelling of free-electrons
  + extension of the QK reaction classes to Martian entry problems   
  
&nbsp;
  
<table cellspacing="0" cellpadding="0">
<tr>
  <td>This work was initiated at the University of Glasgow and was funded for 9 months by <a href="http://www.fluidgravity.co.uk/fgewebsite/">Fluid Gravity Engineering</a> (October 2017 — June 2018).</td>
  <td><img src="https://vincentcasseau.github.io/docs/img/logos/epsrc-sponsor-highres.jpg" width="160%"></td>
</tr>
<tr>
<td style="text-align:center" colspan="2"> Volunteering work from mid-2018 onwards.
</td>
</tr>
</table>  

[**> How-tos**](https://vincentcasseau.github.io/how-tos-dsmc/)  
[**> Tutorials**](https://vincentcasseau.github.io/tutos-dsmcfoam/)  
[**> Source code**](https://github.com/vincentcasseau/hyStrath/tree/master/applications/solvers/discreteMethods/dsmc/dsmcFoam%2B)  
[**> Disclaimer**](https://vincentcasseau.github.io/disclaimer/)  
[**&#x2191; Back to Contents**](#Solvers)
