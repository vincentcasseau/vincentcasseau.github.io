---
layout: page
title: How-tos
subtitle: CFD Module
---

These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/genericCase).  

# Non-equilibrium flow modelling

---  
## 1) Thermal equilibrium

+ The default solver behaviour is to use the two-temperature formulation with multiple vibro-electronic energy pools. In the _thermophysicalProperties_ dictionary, two switches can alter this behaviour to either produce a two-temperature solver with a single vibro-electronic energy pool (_**downgradeToSingleTv**_) or a single-temperature solver (_**downgradeToSingleTemperature**_).  
  
Thus, the single-temperature solver, _hyFoam_, is obtained with  
```c++
    downgradeToSingleTv          no;
    downgradeToSingleTemperature yes;
```  

> The command line for running _hyFoam_ is identical to _hy2Foam_, _i.e._,  
hy2Foam > log.hyFoam&


<div class="paragraph"><p><br>
<br></p></div>

---  
## 2) Thermal non-equilibrium

### 2.1 Two-temperature solver, single vibro-electronic energy pool  
+ The _thermophysicalProperties_ dictionary set-up for this version of _hy2Foam_ is obtained with
```c++
    downgradeToSingleTv          yes;
    downgradeToSingleTemperature no;
```

+ The path to the dictionary dealing with the non-equilibrium aspects is given by  
```c++
    twoTemperatureDictFile "$FOAM_CASE/constant/thermo2TModel";
```

The _thermo2TModel_ dictionary is composed of one subdictionary named _**thermalRelaxationModels**_ that is used for the selection of the energy transfer models, and various subdictionaries that contain the coefficients of these models. For this version of _hy2Foam_, the only transfers that can take place are vibrational-translational (V-T) and heavy-particles - electrons (h-e). If the gas mixture is composed of neutral species only, then h-e energy transfer is disregarded automatically.  
The default subdictionary implementation is as follows

```c++
thermalRelaxationModels
{
    VT
    {
        relaxationType        LandauTellerVT;
        model                 MillikanWhitePark;
        fullCoeffsForm        on;
        overwriteDefault      on;
        speciesDependent      on;
        collidingPair         on;
    }
    
    he
    {
        relaxationType        AppletonBray;
    }
}
```

+ The Landau-Teller equation is used for V-T energy exchange and the V-T relaxation time is dictated by the Millikan-White semi-empirical formula with Park's correction. In the example above, the coefficients for the calculation of the relaxation time are colliding-pair specific and read from one of the subsequent subdictionaries (since _overwriteDefault_ is _on_).

+ The h-e energy transfer process from Appleton & Bray (1963) does not require any input. It can be disabled using a _relaxationType_ defined as _noHEEnergyTransfer_.


### 2.2 Two-temperature solver, multiple vibro-electronic energy pools
+ In the current version of the code, this configuration has several limitations that are as follows    
   - the gas mixture must be composed of neutral particles only  
   - the electronic mode of all particles must be turned off (see [A. §1.2](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#12-disablingenabling-the-electronic-mode-of-a-particle))
   - the molecules must be planar  

+ If the above conditions are fulfilled, then the _thermophysicalProperties_ dictionary set-up is  
```c++
    downgradeToSingleTv          no;
    downgradeToSingleTemperature no;
```

On top of the energy exchange processes described in [§2.1](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#21-two-temperature-solver-single-vibro-electronic-energy-pool), the _thermalRelaxationModels_ subdictionary is augmented with vibrational-vibrational (V-V) and electron-vibrational (e-V) energy transfers.

```c++
thermalRelaxationModels
{
    VV
    {
        relaxationType        KnabVV;
        model                 Knab;
        overwriteDefault      on;
        speciesDependent      on;
        collidingPair         on;
    }
      
    eV
    {
        relaxationType        noeVEnergyTransfer; // not available yet
        model                 BourdonVervisch;
        overwriteDefault      off;
        speciesDependent      off;
    }
}
```

+ The V-V energy transfer process from Knab _et al._ (1992) is the unique V-V model implemented. [Similarly to the V-T model](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Nonequilibrium#21-two-temperature-solver-single-vibro-electronic-energy-pool), it can be made collision-pair specific by switching on the _collidingPair_ boolean.  
V-V energy exchange can be disabled using a _relaxationType_ defined as _noVVEnergyTransfer_. 

+ In this version of _hy2Foam_, species need to be split into different vibro-electronic energy pools.
This is achieved in the _hTCReactions#name_ dictionary with the _**vibTempAssociativity()**_ list. The list order is similar to the _**species()**_ list and the integer value _0_ is reserved to neutral molecules. For a 5-species air:  

```c++
    species
    (
        N2
        O2
        NO
      //N2+
      //O2+
      //NO+
        N
        O
      //N+
      //O+
      //e-
    );

    vibTempAssociativity (0 0 0 1 2);
```
A value of _**1**_ in forth position means that the forth species in the _species()_ list, _**N**_, is grouped into the same vibro-electronic energy pool as the _**1**_ st molecule appearing in the list, here _**N2**_. 

<div class="paragraph"><p><br>
<br></p></div>

---  
## 3) Mean free path and breakdown parameter

These quantities are calculated according to the entries specified in the _transportProperties/rarefiedParameters_ dictionary.

### 3.1 Mean free path  

There are three models (_mfpModel_) available for the computation of the mean free path (mfp) that are: _**maxwellian**_, _**hardSphere**_, and _**variableHardSphere**_.   

You might want to compute the mfp at patches only to speed-up the calculations: indeed, knowledge of the mfp at patches is enough to use the [Smoluchowski temperature jump boundary condition](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Initial-conditions#21-trans-rotational-temperature). To this aim, two booleans (_**computeFieldAndBoundaries**_ and _**computeMfpBoundaries**_) are used and the correct combination is shown below

```c++
rarefiedParameters
{
    computeFieldAndBoundaries      off;
    computeMfpBoundaries           on;
    
    mfpModel                       variableHardSphere;
    writeMfpSpecies                off;
    writeMfpMixture                on;  
}
```

> Always switch _**computeMfpBoundaries**_ on when the Smoluchowski temperature jump and the Maxwell velocity slip BCs are used.

To compute the mfp and other quantities in the whole domain, _**computeFieldAndBoundaries**_ must be switched _on_.  

The species and mixture mfp can be printed using the _**writeMfpSpecies**_ and _**writeMfpMixture**_ booleans.  

### 3.2 Knudsen number 

#### 3.2.1 Overall Knudsen number

The overall Knudsen number, defined as the ratio of the local mean free path to the problem characteristic length (_**characteristicLength**_, in meters) can be computed and printed using the following settings

```c++
rarefiedParameters
{
    computeFieldAndBoundaries      on;
 
    characteristicLength           2.0;
    writeKn_overall                on;
}
```

#### 3.2.2 Breakdown parameter: gradient-length Knudsen number 

The gradient-length Knudsen number, _**KnGLL**_, serves as the breakdown parameter in _hy2Foam_. It is defined as the maximum of four gradient-length Knudsen numbers (called _components_) based on trans-rotational and vibro-electronic temperatures, density, and velocity. It can be printed using the following set-up

```c++
rarefiedParameters
{
    computeFieldAndBoundaries      on;
 
    writeKnGLL                     on;
    writeKnGLL_components          off;   
}
```

<div class="paragraph"><p><br>
<br></p></div>

---  
## 4) Chemistry-vibration coupling

There are two chemistry-vibration models implemented but it is strongly recommended to use the Park TTv model.

### 4.1 Park TTv model

#### 4.1.1 General settings

The subdictionary _**chemistryVibrationCoupling**_ is added to the _chemistryProperties_ dict. Use of the Park TTv model is illustrated below  

```c++
chemistryVibrationCoupling
{
    model ParkTTv;
    
    ParkTTvCoeffs
    {
        exponentTtr         0.7;
        sourceTermModel     preferential;
        
        preferentialModel
        {
            factorType      constant;
            constantFactor  0.3;   
        }
    } 
}
```

For dissociation reactions, Park's temperature is utilised and defined as T_tr^_**exponentTtr**_ x T_ve^(1 - _**exponentTtr**_). A value of 0.7 is usually employed for _**exponentTtr**_. In this example, the _**preferential**_ model is used.   

#### 4.1.2 Reactions dictionary

+ A controlling temperature, _**controlT**_, is added to the _hTCReactions#name_ dictionary. For example, Park's temperature will be used in the following case for forward reaction rate calculations

```c++
controlT dissociation;
```
Other accepted entries for _**controlT**_ can be found in _hTCReactionsEarth93_.


### 4.2 Coupled vibration-dissociation-vibration (CVDV) model

The CVDV model's default settings are as follows 

```c++
chemistryVibrationCoupling
{
    model CVDV;
    
    CVDVCoeffs
    {
        reciprocalU     3;
        simpleHarmonicOscillatorVibCutOff
        {
            N2  34;
            O2  27;
            NO  28;
        }
    }
}
```


<div class="paragraph"><p><br>
<br></p></div>

---  

Contributor: Dr Vincent Casseau
