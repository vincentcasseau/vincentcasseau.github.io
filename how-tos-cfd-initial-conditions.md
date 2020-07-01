These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/genericCase).  

# Initial conditions: the _0/_ folder

---  
## 1) The _include/_ sub-folder

+ To avoid repetitive editing in the _0/_ folder, in particular if there are many species in the gas mixture, a call to a dictionary within the _include/_ sub-folder can be made.
_empty_, _cyclic_, _wedge_, _zeroGradient_, and _symmetry_ patches can be regrouped into _**include/boundaries**_. For example, any field in the _0/_ folder requires a _zeroGradient_ outlet (typical supersonic/hypersonic outlet BC). Below, the outlet patch is omitted and replaced by a call to _boundaries_.

```c++
boundaryField
{ 
    [...]

    #include "include/boundaries"
}
```

In _**include/boundaries**_:  
```c++
outlet
{
    type            zeroGradient;
}
```

+ It is good practice to regroup the initial conditions into a single dictionary
as shown later in [§ 3.1](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions#31-trans-rotational-temperature) using a call to the _**include/initialConditions**_ dictionary and the symbol _**$**_.

The include statement can be placed at the top of file  

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

In _**include/initialConditions**_:

```c++
Ttr       300;
Tve       $Ttr;
TveAtom   0;
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

> This makes running parameterized simulations easier using a bash/python script that will solely edit the _**0/include/initialConditions**_ dictionary entries.

<div class="paragraph"><p><br>
<br></p></div>

---  

## 2) Species mass fractions
  
+ Within the _0/_ folder should be specified all mass fractions of species appearing in the [_**species()**_ list](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Chemistry#12-addingdeleting-species) located in the _**constant/hTCReactions#name**_ dictionary  
+ Naming convention for mass-fraction in OpenFOAM avoids the prefix _Y\__, which means the mass-fraction of _N2_ is simply called _**N2**_.

### 2.1 Non-catalytic wall
+ For a non-catalytic wall, a _zeroGradient_ BC can be used:
```c++
    wall
    {
        type            zeroGradient;
    }
```

### 2.2 Super-catalytic wall
+ For a super-catalytic wall, the mixture composition at the wall is that of the free-stream and the current implementation is as follows:  
```c++
    inlet
    {
        type            fixedValue;
        value           uniform $Y_#nameSpecies;
    }

    wall
    {
        type            fixedValue;
        value           uniform $Y_#nameSpecies;
    }
```


<div class="paragraph"><p><br>
<br></p></div>

---  

## 3) Temperature fields

### 3.1 Trans-rotational temperature
+ The trans-rotational temperature field is named _**Tt**_  and must be present in the _0/_ folder
+ Its implementation in the _0/_ folder is identical to the standard temperature field in OpenFOAM, except for the Smoluchowski temperature jump boundary condition.  
+ The Smoluchowski temperature jump boundary condition for the trans-rotational counterpart writes as follows
```c++
    wall
    {
        type            nonEqSmoluchowskiJumpT;
        accommodationCoeff 1;
        Twall           uniform $Twall;
        value           $Twall;
    }
```

### 3.2 Vibro-electronic temperature

#### 3.2.1 Single vibro-electronic energy pool formulation  
+ Please refer to [D. §2.1](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#21-two-temperature-solver-single-vibro-electronic-energy-pool) if you are not familiar with this code feature   
+ The mixture vibro-electronic temperature field is called _**Tv**_ and must be present in the _0/_ folder
+ The Smoluchowski temperature jump boundary condition for the mixture vibro-electronic counterpart writes as follows
```c++
    wall
    {
        type            nonEqSmoluchowskiJumpTvMix;
        accommodationCoeff 1;
        Twall           uniform $Twall;
        value           $Twall;
    }
```


#### 3.2.2 Multiple vibro-electronic energy pools formulation  
+ Please refer to [D. §2.2](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#22-two-temperature-solver-multiple-vibro-electronic-energy-pools) if you are not familiar with this code feature  
+ The species vibro-electronic temperature fields are called _**Tv\_#nameSpecies**_. There are as many _**Tv\_#nameSpecies**_ fields to define in the _0/_ folder as there are species in the _**species()**_ list.  
+ The Smoluchowski temperature jump boundary condition for the species (molecule) vibro-electronic temperature writes as follows
```c++
    wall
    {
        type            nonEqSmoluchowskiJumpTv;
        accommodationCoeff 1;
        Twall           uniform $Twall;
        value           $Twall;
    }
```


<div class="paragraph"><p><br>
<br></p></div>

---  

## 4) Velocity field

+ The Maxwell velocity slip boundary condition has been slightly re-written (the [mean free path](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#3-mean-free-path-and-breakdown-parameter) now depends upon the model retained in _transportProperties_ dictionary) and is defined as 

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

+ The velocity at the inlet patch can increase linearly with time from an _**offset**_ value up to a velocity whose components are given by the entry _**refValue**_, components that can then be multiplied by the _**amplitude**_.
For example, for a linear 1e-4 sec long increase in velocity from 50 m/s up to 1000 m/s with no angle of attack nor slip angle (_**U**_ is thus aligned with the x-axis: (1 0 0)), then the new _**rampInlet**_ boundary condition is

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

To use the _**rampInlet**_ boundary condition, a line should be added into the _system/controlDict_ dictionary  
```c++
libs ("libstrathFiniteVolume.so");
```

<div class="paragraph"><p><br>
<br></p></div>

---

##### Contributor: Dr Vincent Casseau