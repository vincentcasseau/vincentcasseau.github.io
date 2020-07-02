---
layout: page
title: How-tos
subtitle: CFD Module
nav-short: true
---

These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/genericCase).  

# Chemistry modelling

---

## 1) Multi-species flow

### 1.1 The _chemDicts/_ folder
+ Within the _constant/_ directory, the _chemDicts/_ folder regroups default chemistry dictionaries. It is preferable not to modify the original files. Thus, a copy of the most appropriate _hTCReactions#name_ dictionary can be made into the _constant/_ folder.
+ The path to the _hTCReactions#name_ dictionary needs to be edited accordingly in _thermophysicalProperties_. This done with the entry _foamChemistryFile_ that can be defined as  
```c++
    foamChemistryFile        "$FOAM_CASE/constant/hTCReactions#name";
```

Available _hTCReactions#name_ dictionaries are

| Chemistry dict name    | Reference
|:-------------:|:-------------:|
| _hTCReactionsEarth93_      |  Park _et al._, 1993 |
| _hTCReactionsMars74_      |  Evans, Schexnayder & Grose, 1974          |
| _hTCReactionsMars94_      |  Park _et al._, 1994           |
| _hTCReactionsDK_      |  Dunn & Kang, 1973          |
| _hTCReactionsES_      |  Evans & Schexnayder, 1980          |
| _hTCReactionsJ92_      |  Jachimowski, 1992           |
| _hTCReactionsJ92\_fwd_      |  Jachimowski, forward reactions only, 1992           |
| _hTCReactionsQK_      |  Quantum-kinetics, Scanlon _et al._, 2015      |


### 1.2 Adding/deleting species   
+ In the _hTCReactions#name_ dictionary, the species composing the gas mixture need to be uncommented in the _species_ list entry. For a 5-species air mixture:    
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
```
As illustrated in the example, a specific order should be respected  
1. molecules  
2. charged molecules  
3. atoms  
4. charged atoms  
5. electrons  

+ In the _thermoDEM_ dictionary, uncomment all species listed in the _hTCReactions#name_ dictionary (**and comment out those which are not present**)
+ All species listed in the _hTCReactions#name_ dictionary should also be present in the _0/_ directory. This is discussed in [G. Initial conditions](https://vincentcasseau.github.io/how-tos-cfd-initial-conditions/).

### 1.3 Printing species quantities  
+ In the _hTCProperties_ dictionary, switch on/off any of those booleans to print the desired fields  
```c++
mixtureOutputs
{
    molarFraction       off;
    numberDensity       off;
    partialDensity      off;
    partialPressure     off;
    degreesOfFreedom    off;
    vibrationalEnergy   off;
}
```

<div class="paragraph"><p><br>
<br></p></div>

---

## 2) Non-reacting flow

### 2.1 Disable chemistry  
+ In the _hTCProperties_ dictionary, switch off the _active_ boolean as follows    
```c++
     active          off;
```  

<div class="paragraph"><p><br>
<br></p></div>

---  
## 3) Chemically-reacting flow  

### 3.1 Enable chemistry
+ In the _hTCProperties_ dictionary, switch on the _active_ boolean as follows    
```c++
     active          on;
```  

+ In the _chemistryProperties_ dictionary, the same operation should be repeated with the _chemistry_ boolean  
```c++
     chemistry          on;
```

> In this dictionary, the _initialChemicalTimeStep_ entry is not used by the solvers yet.  

### 3.2 Implementing a chemical reaction  
#### 3.2.1 Forward reaction  
+ Within the _hTCReactions#name_ dictionary, the _reactions_ subdictionary is enumerating the different chemical reactions to consider. The modified Arrhenius law coefficients are given in the table below

| Coefficient    | Meaning | Units |
|:-------------:|:-------------|:------:|
| _A_      |  pre-exponential factor | m^3 kmol^-1 s^-1 |
| _beta_      |  temperature exponent          |   -     |
| _Ta_      |  temperature of activation           |   K    |

__Please pay attention to the units of the pre-exponential factor, *A*.__ 

+ The reaction _type_ is defined as __*irreversibleArrheniusReaction*__.

```c++
reactions
{
    // Reaction no 1
    oxygenAtomicNitrogenReaction
    {
        type     irreversibleArrheniusReaction;
        reaction "O2 + N = 2O + N";
        A        1.0e19;
        beta     -1.5;
        Ta       59500; 
    }
}
```


#### 3.2.2 Reverse reaction   
+ Extra coefficients entering into the calculation of the reverse reaction rate constant [Park, 1990], _k\_rev_, are given below  

| Extra coefficient    | Meaning | Units |
|:-------------:|:-------------|:------:|
| _ni()_      |  mixture number density list | m^-3 |
| _A0()_ - _A4()_      | Park's coefficients for _k\_rev_  |   -    |
 
+ In the _hTCReactions#name/reactions_ dictionary, the reaction _type_  can either be __*reversibleArrheniusReaction*__ or __*nonEquilibriumReversibleArrheniusReaction*__. Their implementation is exemplified hereafter    

```c++
reactions
{
    // Reaction no 1
    oxygenAtomicNitrogenReaction
    {
        type     reversibleArrheniusReaction;
        reaction "O2 + N = 2O + N";
        A        1.0e19;
        beta     -1.5;
        Ta       59500;
        
        ni       (1e20 1e21 1e22 1e23 1e24 1e25);
        A0       (1.8103 0.91354 0.64183 0.55388 0.52455 0.50989);
        A1       (1.9607 2.316 2.4253 2.46 2.4715 2.4773);
        A2       (3.5716 2.2885 1.9026 1.7763 1.7342 1.7132);
        A3       (-7.3623 -6.7969 -6.6277 -6.572 -6.5534 -6.5441);
        A4       (0.083861 0.046338 0.035151 0.031445 0.030209 0.029591);  
    }

    // Reaction no 2
    hydrogenAtomOxygenReaction
    {
        type     nonEquilibriumReversibleArrheniusReaction;
        reaction "H + O2 = OH + O";
        forward
        {
            A        2.2e11;
            beta     0;
            Ta       8454;
        }
        reverse
        {
            A        1.42e4;
            beta     0;
            Ta       1664;
        }
    }
}
```

#### 3.2.3 Third-body interaction  
In the _hTCReactions#name/reactions_ dictionary, the _type_ of the reaction is modified to either _**irreversiblethirdBodyArrheniusReaction**_, _**reversiblethirdBodyArrheniusReaction**_, or _**nonEquilibriumReversiblethirdBodyArrheniusReaction**_. An example is given below and many more can be found in the _chemDicts/_ folder.  

```c++
reactions
{
    // Reaction no 1
    oxygenTBReaction
    {
        type     reversiblethirdBodyArrheniusReaction;
        reaction "O2 + M = 2O + M";
        A        2.0e18;
        beta     -1.5;
        Ta       59500;
        coeffs
        (
            ("N2" 1.0)
            ("O2" 1.0)
            ("NO" 1.0)
          //("N2+" 1.0)
          //("O2+" 1.0)
          //("NO+" 1.0)
            ("N" 5.0)
            ("O" 5.0)
          //("N+" 5.0)
          //("O+" 5.0)
          //("e-" 0.0)
        );
        
        ni       (1e20 1e21 1e22 1e23 1e24 1e25);
        A0       (1.8103 0.91354 0.64183 0.55388 0.52455 0.50989);
        A1       (1.9607 2.316 2.4253 2.46 2.4715 2.4773);
        A2       (3.5716 2.2885 1.9026 1.7763 1.7342 1.7132);
        A3       (-7.3623 -6.7969 -6.6277 -6.572 -6.5534 -6.5441);
        A4       (0.083861 0.046338 0.035151 0.031445 0.030209 0.029591);  
    }
}
```
**NB:** All species present in the _species_() list must be present in the _coeff_() list, no more, no less. 

### 3.3  Increase robustness
Backward reaction rates may sometimes cause problems in the low-temperature regions and yield the simulation to crash. A minimum temperature value, _Tmin_, can be introduced into the rate calculations to increase robustness [Scalabrin, 2007]. A switch called _**modifiedTemperature**_ located in the _chemistryProperties_ dictionary is there for this purpose.

```c++
modifiedTemperature on;
modifiedTemperatureCoeffs
{
    Tmin      800.0;
    epsilon   80.0;
}
```

<div class="paragraph"><p><br>
<br></p></div>

---  

## 4) To go further: chemistry-vibration coupling  
This aspect is detailed in [D. Nonequilibrium](https://vincentcasseau.github.io/how-tos-cfd-nonequilibrium/#4-chemistry-vibration-coupling).
