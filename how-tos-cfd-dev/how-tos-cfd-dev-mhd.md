---
layout: page
title: How-tos
subtitle: CFD Module - Next Release
nav-short: true
---

This how-to is based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/dev-isro-1/run/hyStrath/hy2MhdFoam/NASA_MSL_forebody_NR-MHD).  

# MHD modelling

---
## 1) Enabling/disabling MHD

In the <dirname>constant/</dirname> folder, the <dict>mhdProperties</dict> dictionary is listing all the MHD parameters. 

```c++
/*--------------------------------*- C++ -*----------------------------------*\
| =========                 |                                                 |
| \\      /  F ield         | OpenFOAM: The Open Source CFD Toolbox           |
|  \\    /   O peration     | Version:  v1706                                 |
|   \\  /    A nd           | Web:      www.OpenFOAM.com                      |
|    \\/     M anipulation  |                                                 |
\*---------------------------------------------------------------------------*/
FoamFile
{
    version     2.0;
    format      ascii;
    class       dictionary;
    location    "constant";
    object      mhdProperties;
}
// * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //

active          true;

mhdModel        lowReMag;

hallEffect      true;

electricalConductivityModel Bush;

constantElectricalConductivityCoeffs
{
    value           5100;
}

BushCoeffs
{
    sigma0          5100;
    T0              12000;
    n               2;
}


// ************************************************************************* //
```

The first switch, <dictkey>active</dictkey>, can be used to enable or disable MHD.  


<!--<p>When `a != 0`, there are two solutions to `ax^2 + bx + c = 0` and-->
<!--they are</p>-->
<!--<p style="text-align:center">-->
<!--  `x = (-b +- sqrt(b^2-4ac))/(2a) .`-->
<!--</p>-->

<br>

---
## 2) MHD models

<br>

---
## 3) Electrical conductivity models

<br>

---
## 4) Creation of the initial magnetic field


<br>

---
## 5) Hall effect


<br>
  
--- 

[**< E. Turbulence modelling**](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev-turbulence/)  
[**> G. Initial conditions**](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev-initial-conditions/)  
[**&#x2191; Back to Contents**](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev/)
