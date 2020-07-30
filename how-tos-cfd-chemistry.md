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

### 1.1 The chemDicts/ folder
In the <dirname>constant/</dirname> directory, the <dirname>chemDicts/</dirname> folder is gathering default chemistry dictionaries. It is advised not to modify the original files for future reference. Thus, a copy of the most appropriate <dict>hTCReactions#name</dict> dictionary can be made into the <dirname>constant/</dirname> folder.  

The path to the <dict>hTCReactions#name</dict> dictionary needs to be edited accordingly in <dict>thermophysicalProperties</dict>. This done using the  <dictkey>foamChemistryFile</dictkey> entry as  

```c++
    foamChemistryFile        "$FOAM_CASE/constant/hTCReactions#name";
```

Available <dict>hTCReactions#name</dict> dictionaries are

| Chemistry dict name    | Reference
|:-------------:|:-------------:|
| <dict>hTCReactionsEarth93</dict>      |  Park _et al._, 1993 |
| <dict>hTCReactionsMars74</dict>      |  Evans, Schexnayder & Grose, 1974          |
| <dict>hTCReactionsMars94</dict>      |  Park _et al._, 1994           |
| <dict>hTCReactionsDK</dict>      |  Dunn & Kang, 1973          |
| <dict>hTCReactionsES</dict>      |  Evans & Schexnayder, 1980          |
| <dict>hTCReactionsJ92</dict>      |  Jachimowski, 1992           |
| <dict>hTCReactionsJ92_fwd</dict>      |  Jachimowski, forward reactions only, 1992           |
| <dict>hTCReactionsQK<dict>      |  Quantum-kinetics, Scanlon _et al._, 2015      |

&nbsp;  

### 1.2 Adding/deleting species   
In the <dict>hTCReactions#name</dict> dictionary, the species composing the gas mixture need to be uncommented in <dictkey>species()</dictkey>. For a 5-species air mixture  
 
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

As shown in this example, a specific order must be respected  
1. molecules  
2. charged molecules  
3. atoms  
4. charged atoms  
5. electrons  

In the <dict>thermoDEM</dict> dictionary, uncomment all species listed in the <dict>hTCReactions#name</dict> dictionary - **and comment out those that are not present**.  
All species listed in the <dict>hTCReactions#name</dict> dictionary should also be present in the <dirname>0/</dirname> directory. This is discussed in [G. Initial conditions](https://vincentcasseau.github.io/how-tos-cfd-initial-conditions/#2-species-mass-fractions).

### 1.3 Printing species quantities  
In the <dict>hTCProperties</dict> dictionary, switch <dictval>on</dictval>/<dictval>off</dictval> any of these booleans to print the desired fields 
 
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

<br>

---

## 2) Non-reacting flow

### 2.1 Disable chemistry  
In the <dict>hTCProperties</dict> dictionary, switch <dictval>off</dictval> the <dictkey>active</dictkey> boolean as follows   
 
```c++
     active          off;
```  

<br>

---  
## 3) Chemically-reacting flow  

### 3.1 Enable chemistry
In the <dict>hTCProperties</dict> dictionary, switch <dictval>on</dictval> the <dictkey>active</dictkey> boolean as follows 
   
```c++
     active          on;
```  

In the <dict>chemistryProperties</dict> dictionary, the same operation must be repeated with the <dictkey>chemistry</dictkey> switch  

```c++
     chemistry          on;
```

> In this dictionary, the <dictkey>initialChemicalTimeStep</dictkey> entry is not used by the solvers yet.  

### 3.2 Implementing a chemical reaction  
#### 3.2.1 Forward reaction  
In the <dict>hTCReactions#name</dict> dictionary, the <subdict>reactions</subdict> subdictionary is enumerating the different chemical reactions to consider. The modified Arrhenius law coefficients are given in the table below

| Coefficient    | Meaning | Units |
|:-------------:|:-------------|:------:|
| <dictkey>A</dictkey>      |  pre-exponential factor | m^3 kmol^-1 s^-1 |
| <dictkey>beta</dictkey>      |  temperature exponent          |   -     |
| <dictkey>Ta</dictkey>      |  temperature of activation           |   K    |

> Please pay attention to the units of the pre-exponential factor, <dictkey>A</dictkey>, when customising your own <dict>hTCReactions#name</dict> dictionary.

The reaction <dictkey>type</dictkey> is defined as <dictval>irreversibleArrheniusReaction</dictval>.

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

&nbsp;

#### 3.2.2 Reverse reaction   
Additional coefficients entering into the calculation of the reverse reaction rate constant [Park, 1990], _k\_rev_, are given below  

| Extra coefficient    | Meaning | Units |
|:-------------:|:-------------|:------:|
| <dictkey>ni()</dictkey>      |  mixture number density list | m^-3 |
| <dictkey>A0()</dictkey> - <dictkey>A4()</dictkey>      | Park's coefficients for _k\_rev_  |   -    |
 
In the <dict>hTCReactions#name/</dict><subdict>reactions</subdict> dictionary, the reaction <dictkey>type</dictkey>  can either be <dictval>reversibleArrheniusReaction</dictval> or <dictval>nonEquilibriumReversibleArrheniusReaction</dictval>. Their implementation is exemplified hereafter    

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
        A1       (8.8685 9.2238 9.3331 9.3678 9.3793 9.3851);
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

&nbsp;

#### 3.2.3 Third-body interaction  
In the <dict>hTCReactions#name/</dict><subdict>reactions</subdict> dictionary, the <dictkey>type</dictkey> of the reaction is modified to either <dictval>irreversiblethirdBodyArrheniusReaction</dictval>, <dictval>reversiblethirdBodyArrheniusReaction</dictval>, or <dictval>nonEquilibriumReversiblethirdBodyArrheniusReaction</dictval>. An example is given below and many more can be found in the <dirname>chemDicts/</dirname> folder.  

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
        A1       (8.8685 9.2238 9.3331 9.3678 9.3793 9.3851);
        A2       (3.5716 2.2885 1.9026 1.7763 1.7342 1.7132);
        A3       (-7.3623 -6.7969 -6.6277 -6.572 -6.5534 -6.5441);
        A4       (0.083861 0.046338 0.035151 0.031445 0.030209 0.029591);  
    }
}
```
> All species present in the <dictkey>species()</dictkey> list must be present in the <dictkey>coeff()</dictkey> list, no more, no less. 

### 3.3  Increase robustness
Backward reaction rates may sometimes cause problems in low-temperature regions and yield the simulation to crash. A minimum temperature value, <dictkey>Tmin</dictkey>, can be introduced into the rate calculations to increase robustness [Scalabrin, 2007]. A switch called <dictkey>modifiedTemperature</dictkey> located in the <dict>chemistryProperties</dict> dictionary is there for this purpose.

```c++
modifiedTemperature on;
modifiedTemperatureCoeffs
{
    Tmin      800.0;
    epsilon   80.0;
}
```

<br>

---  

## 4) To go further: chemistry-vibration coupling  
This aspect is detailed in [D. Nonequilibrium](https://vincentcasseau.github.io/how-tos-cfd-nonequilibrium/#4-chemistry-vibration-coupling).

<br>
  
--- 

[**< B. Transport modelling**](https://vincentcasseau.github.io/how-tos-cfd-transport/)  
[**> D. Non-equilibrium flow modelling**](https://vincentcasseau.github.io/how-tos-cfd-nonequilibrium/)  
[**&#x2191; Back to Contents**](https://vincentcasseau.github.io/how-tos-cfd/)
