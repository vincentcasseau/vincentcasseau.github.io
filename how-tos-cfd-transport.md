---
layout: page
title: How-tos
subtitle: CFD Module
---

These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/genericCase).  

# Transport modelling

<br>

---

## 1) Individual shear viscosity and thermal conductivity

### 1.1 Inviscid simulation    
+ In the _thermophysicalProperties/thermoType_ dictionary, edit the _transport_ entry to __*constant*__
+ In the _thermoDEM/#nameSpecies/transport/constant_ dictionary, for all #nameSpecies present in the gas mixture, edit the value of the entry _mu_ to be __*0*__

### 1.2 Viscous simulation with constant shear viscosity and thermal conductivity
+ In the _thermophysicalProperties/thermoType_ dictionary, edit the _transport_ entry to __*constant*__
+ In the _thermoDEM/#nameSpecies/transport/constant_ dictionary, for all #nameSpecies present in the gas mixture, edit the value of the entry _mu_ to the desired value
+ The thermal conductivity is then calculated using Eucken's formula

### 1.3 To go further
The names of all valid entries for the _transport_ keyword in the _thermophysicalProperties/thermoType_ dictionary are  

| Transport model name    | Parameters          |
|:-------------:|-------------|
| _constant_      | _mu_ |
| _SutherlandEucken_      | _As_, _Ts_     |
| _BlottnerEucken_ | _A_, _B_, _C_     |
| _CEA_      | _temp()_, _visco()_, _kappa()_      |
| _powerLawEucken_ | _diameter_, _omega_     |

> The coefficients of these models are to be found in the _thermoDEM/#nameSpecies_ dictionary. The first four models are employing coefficients located into the _transport_ subdictionary, while the _powerLawEucken_ model is using the species diameter, _diameter_, and species temperature exponent of viscosity, _omega_, located in the _specie_ subdictionary.

### 1.4 Print species shear viscosity and thermal conductivity
In the _transportProperties/transportModels_ dictionary, edit any of the following booleans to _**on**_  
```c++
    writeViscositySpecies          on;  
    writeThermalConducSpecies      on; 
```

<div class="paragraph"><p><br>
<br></p></div>

---

## 2) Mixing rules

The available mixing rules are  

| Mixing rule name    | Parameters          |
|:-------------:|:-------------:|
| _molar_      | - |
| _Wilke_      | - |
| _ArmalySutton_ | _correctedArmalySutton_    |

and can be chosen editing the entry _mixingRule_ in the _transportProperties/transportModels_ dictionary. The mixture shear viscosity and thermal conductivity can be printed by reproducing the procedure described in [§1.4](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#14-print-species-shear-viscosity-and-thermal-conductivity):  
```c++
    writeViscosityMixture          on;  
    writeThermalConducMixture      on; 
```

<div class="paragraph"><p><br>
<br></p></div>

---

## 3) Mass diffusion

### 3.1 Disable multi-species diffusion
In the _transportProperties/transportModels_ dictionary, edit the following entries to  
```c++
    multiSpeciesTransport         noSpeciesDiffusion;  
    binaryDiffusivityModel        noBinaryDiffusivityModel;
```

### 3.2 Lewis number model
In the _transportProperties/transportModels_ dictionary, edit the following entries to  
```c++
    multiSpeciesTransport         LewisNumber;  
    binaryDiffusivityModel        noBinaryDiffusivityModel;
```

The Lewis number value can be found in the _diffusiveFluxesParameters_ subdictionary.  

### 3.3 Fick's law and binary diffusion models
In the _transportProperties/transportModels_ dictionary, edit the following entries to  
```c++
    multiSpeciesTransport         Fick; 
``` 

Available models for the calculation of binary diffusion coefficients are  

| Binary diffusion model name    | Parameters          |
|:-------------:|-------------|
| _constant_      | _constantBinaryDiffusivityModelCoefficients_ |
| _GuptaD_      | _yearGuptaModel_, _collisionData_ dict     |
| _GuptaO_ | _yearGuptaModel_, _collisionData_ dict     |
| _Stephani_ | _molWeight_, _diameter_, _omega_     |

> The _constantBinaryDiffusivityModelCoefficients_ and _yearGuptaModel_ entries can be found in the _diffusiveFluxesParameters_ subdictionary. _yearGuptaModel_ accepted values are "1989" or "1990". Please refer to the _collisionData_ dictionary for the correct combination.


Ex:  
```c++
binaryDiffusivityModel       GuptaD;  
  
diffusiveFluxesParameters   
{  
     yearGuptaModel          "1989";   
}  
  
collisionData  
{  
     neutralNeutralInteractions  
     { 
          Gupta1989D
          {
               Dbar
               {
                    N2_N2 (0.0 0.0112 1.16182 -11.3091);  
                    N2_O2 (0.0 0.0465 0.9271 -8.1137);         
               }
          } 
     }  
}  
```  

### 3.4 SCEBD model 
In the _transportProperties/transportModels_ dictionary, edit the following entry to  
```c++
    multiSpeciesTransport         SCEBD; 
``` 

Please refer to [§3.3](https://github.com/vincentcasseau/hyStrath/wiki/How-to-::-Transport#33-ficks-law) for the list of available binary diffusion coefficient models.

### 3.5 Additional features (to Fick and SCEBD models)
- Results using the non-corrected forms of Fick's law and the SCEBD model can be obtained by switching on the _useNonCorrectedForm_ boolean located in the _diffusiveFluxesParameters_ subdictionary (for comparison with the corrected form only). It is turned to *off* by default, which means that the sum of the diffusive fluxes is zero.

> The _useNonCorrectedForm_ entry can be deleted from the _diffusiveFluxesParameters_ subdictionary if you wish (safer).

- In the same subdictionary, the _addPressureGradientTerm_ boolean adds on the effect of the pressure gradient.

<div class="paragraph"><p><br>
<br></p></div>

---

Contributor: Dr Vincent Casseau
