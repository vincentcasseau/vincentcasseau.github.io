---
layout: page
title: How-tos
subtitle: CFD Module - Next release
nav-short: true
---

These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/dev-isro-1/run/hyStrath/hy2Foam/genericCase).  

# Initial conditions: the 0/ folder

---  
## 1) The include/ sub-folder

A call to a dictionary located in the <dirname>0/include/</dirname> sub-folder can be made to avoid editing multiple files in the <dirname>0/</dirname> directory, in particular if the gas mixture is composed of many species. <dictval>empty</dictval>, <dictval>cyclic</dictval>, <dictval>wedge</dictval>, <dictval>zeroGradient</dictval>, and <dictval>symmetry</dictval> boundary patches can be put into <dirname>include/</dirname><dict>boundaries</dict>. For instance, most fields in the <dirname>0/</dirname> folder require a <dictval>zeroGradient</dictval> outlet boundary condition (BC) and this patch can thus be replaced by a call to <dict>boundaries</dict>, as shown below

```c++
boundaryField
{ 
    [...]

    #include "include/boundaries"
}
```

In <dirname>include/</dirname><dict>boundaries</dict>, the outlet BC would then be written as follows
  
```c++
outlet
{
    type            zeroGradient;
}
```

Similarly, it can become handy to group the initial conditions into a single file by calling the <dirname>include/</dirname><dict>initialConditions</dict> dictionary and using the _**$**_ symbol. The *include* statement can be placed at the top of each file  

```c++
FoamFile
{
    version     2.0;
    format      ascii;
    class       volVectorField;
    object      U;
}
// * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //

#include "include/initialConditions"

dimensions      [0 1 -1 0 0 0 0];

internalField   uniform $velocityField;

boundaryField
{
    [...]
}
```

After repeating this operation for every field in the <dirname>0/</dirname> folder, the <dirname>include/</dirname><dict>initialConditions</dict> dictionary may be defined as follows

```c++
Ttr       300;
Tve       $Ttr;
Twall     810;

pressure  5.18655;

UxInlet 1.131e4;
velocityInlet  ($UxInlet 0 0);
velocityField  (0 0 0);
velocityWall   (0 0 0);

Y_N2      0.767;
Y_O2      0.233;
Y_NO      0;
Y_N       0;
Y_O       0;
```

> A simple bash or python script can edit the entries of this single dictionary and running parameterized simulations becomes much easier.

<br>

---  
## 2) Species mass or molar fractions
  
Either the mass or molar fractions of all species appearing in the [_**species()**_ list](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev-chemistry/#12-addingdeleting-species) must be given in the <dirname>0/</dirname> folder. OpenFOAM's naming convention for mass fractions omits the prefix "_Y\__", which means that the mass fraction of species _N2_ is simply called _**N2**_.

To initialise the simulation using molar fractions instead, rename the species files with the prefix "_X\__", for example: _**X_N2**_. The <dirname>include/</dirname><dict>initialConditions</dict> dictionary may then be defined to contain

```c++
X_N2      0.79;
X_O2      0.21;
```

When both species mass and molar fractions are given in a time folder, the simulation will (re)start using the species mass fractions.

### 2.1 Non-catalytic wall
A non-catalytic wall BC can be set-up using the <dictval>zeroGradient</dictval> wall boundary type  

```c++
    wall
    {
        type            zeroGradient;
    }
```

&nbsp;

### 2.2 Super-catalytic wall
For a super-catalytic wall, the mixture composition at the surface is that of the free-stream and its implementation is as follows
  
```c++
    inlet
    {
        type            fixedValue;
        value           uniform $Y_#speciesName;
    }

    wall
    {
        type            fixedValue;
        value           uniform $Y_#speciesName;
    }
```

<br>

---  
## 3) Temperature fields

### 3.1 Trans-rotational temperature
The trans-rotational temperature field is printed as _**Tt**_  and must always be present in the <dirname>0/</dirname> folder.
Its implementation is identical to the temperature field in all official OpenFOAM solvers, except for the Smoluchowski temperature jump boundary condition. Some examples are given hereafter.  

+ An isothermal wall
```c++
    wall
    {
        type            fixedValue;
        value           uniform $Twall;
    }
```
+ An adiabatic wall
```c++
    wall
    {
        type            zeroGradient;
    }
```
+ A wall with the Smoluchowski trans-rotational temperature jump BC
```c++
    wall
    {
        type            nonEqSmoluchowskiJumpT;
        accommodationCoeff 1;
        Twall           uniform $Twall;
        value           $Twall;
    }
```

&nbsp;

### 3.2 Vibro-electronic temperature

#### 3.2.1 Single vibro-electronic energy pool formulation  
Please refer to [D. §2.1](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev-nonequilibrium/#21-single-vibro-electronic-energy-pool) if you are not familiar with this code feature.  
   
The mixture vibro-electronic temperature field is called _**Tv**_ and must be present in the <dirname>0/</dirname> folder.
The Smoluchowski vibro-electronic temperature jump BC is written as follows  

```c++
    wall
    {
        type            nonEqSmoluchowskiJumpTvMix;
        accommodationCoeff 1;
        Twall           uniform $Twall;
        value           $Twall;
    }
```

&nbsp;

#### 3.2.2 Multiple vibro-electronic energy pools formulation  
Please refer to [D. §2.2](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev-nonequilibrium/#22-multiple-vibro-electronic-energy-pools) if you are not familiar with this code feature.
  
The species vibro-electronic temperature fields are called _**Tv\_#speciesName**_ and there are as many fields as there are species in the <dictkey>species()</dictkey> list.
The Smoluchowski vibro-electronic temperature jump BC for molecule species is defined as

```c++
    wall
    {
        type            nonEqSmoluchowskiJumpTv;
        accommodationCoeff 1;
        Twall           uniform $Twall;
        value           $Twall;
    }
```

<br>

---  
## 4) Velocity field

### 4.1 Maxwell velocity slip
The Maxwell velocity slip BC has been slightly re-written (the [mean free path](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev-nonequilibrium/#3-mean-free-path-and-breakdown-parameter) is now calculated according to the model chosen in the <dict>transportProperties</dict> dictionary) and is given by 

```c++
    wall
    {
        type            nonEqMaxwellSlipU;
        accommodationCoeff 1;
        Uwall           $velocityWall;
        refValue        uniform $velocityWall;
        valueFraction   uniform 1.0;
        thermalCreep    true;
        curvature       true;
        value           uniform $velocityWall;
    }
```

&nbsp;

### 4.2 Linear inlet ramp
The velocity at an inflow patch can be set to increase linearly with time from an <dictkey>offset</dictkey> value up to a velocity whose components are given by the entry <dictkey>refValue</dictkey>, components that are then multiplied by the <dictkey>amplitude</dictkey> scalar.  

For example, a 0.1 ms-long linear increase in velocity from 50 m/s to 1000 m/s with no angle of attack nor slip angle (_**U**_ is thus aligned with the x-axis: (1 0 0)) is obtained by setting up the <dictkey>rampInlet</dictkey> BC as

```c++
    inlet
    {
        type            rampInlet;
        refValue        uniform (1 0 0);
        offset          (50 0 0);
        amplitude       1000;
        tRamp           1e-4;
    }
```

To use the <dictkey>rampInlet</dictkey> BC, one line should be added to the <dirname>system/</dirname><dict>controlDict</dict> dictionary 
 
```c++
libs ("libstrathFiniteVolume.so");
```

<br>
  
--- 

[**< F. MHD modelling**](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev-mhd/)  
[**> H. Advanced features**](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev-advanced/)  
[**&#x2191; Back to Contents**](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev/)
