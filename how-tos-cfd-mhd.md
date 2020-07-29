---
layout: page
title: How-tos
subtitle: CFD Module
nav-short: true
---

This how-to is based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2MhdFoam/NASA_MSL_forebody_NR-MHD).  

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

mhd             true;

mhdModel        lowReMag;

collisionData   constant;

conductivityModel Bush;

T0              12000;

n               2;

sigma0          5100;

hallEffect      true;


// ************************************************************************* //
```

The first switch, <dictkey>mhd</dictkey>, can be used to enable or disable MHD.  


When $a \ne 0$, there are two solutions to \(ax^2 + bx + c = 0\) and they are
$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$


<p>When `a != 0`, there are two solutions to `ax^2 + bx + c = 0` and
they are</p>
<p style="text-align:center">
  `x = (-b +- sqrt(b^2-4ac))/(2a) .`
</p>

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
