---
layout: page
title: How-tos
subtitle: CFD Module
nav-short: true
---

These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/genericCase).  

# Transport modelling

---
## 1) Individual shear viscosity and thermal conductivity

### 1.1 Inviscid simulation    
In the <dict>thermophysicalProperties/</dict><subdict>thermoType</subdict> dictionary, edit the <dictkey>transport</dictkey> entry to <dictval>constant</dictval>.

In the <dict>thermoDEM/</dict><subdict>#speciesName/transport/constant</subdict> dictionary, for all #speciesName present in the gas mixture, edit the value of the entry <dictkey>mu</dictkey> to be <dictval>0</dictval>.

### 1.2 Viscous simulation with constant shear viscosity and thermal conductivity
+ In the <dict>thermophysicalProperties/</dict><subdict>thermoType</subdict> dictionary, edit the <dictkey>transport</dictkey> entry to <dictval>constant</dictval>.
+ In the <dict>thermoDEM/</dict><subdict>#speciesName/transport/constant</subdict> dictionary, for all #speciesName present in the gas mixture, edit the value of the entry <dictkey>mu</dictkey> to the desired value.
+ The thermal conductivity is then calculated using Eucken's formula.

### 1.3 Other transport models
The names of all valid entries for the <dictkey>transport</dictkey> keyword in the <dict>thermophysicalProperties/</dict><subdict>thermoType</subdict> dictionary are  

| Transport model name    | Parameters          |
|:-------------:|-------------|
| _constant_      | _mu_ |
| _SutherlandEucken_      | _As_, _Ts_     |
| _BlottnerEucken_ | _A_, _B_, _C_     |
| _CEA_      | _temp()_, _visco()_, _kappa()_      |
| _powerLawEucken_ | _diameter_, _omega_     |

The coefficients of these models are to be found in the <dict>thermoDEM/</dict><subdict>#speciesName</subdict> dictionary. The first four models are employing coefficients located into the <subdict>transport</subdict> subdictionary, while the _powerLawEucken_ model is using the species diameter, _diameter_, and species temperature exponent of viscosity, _omega_, located in the <subdict>specie</subdict> subdictionary.

### 1.4 Print species shear viscosity and thermal conductivity
In the <dict>transportProperties/</dict><subdict>transportModels</subdict> dictionary, edit any of the following booleans to <dictval>on</dictval>  

```c++
    writeViscositySpecies          on;  
    writeThermalConducSpecies      on; 
```

<br>

---
## 2) Mixing rules

The available mixing rules are  

| Mixing rule name    | Parameters          |
|:-------------:|:-------------:|
| _molar_      | - |
| _Wilke_      | - |
| _ArmalySutton_ | _correctedArmalySutton_    |

and can be chosen editing the entry <dictkey>mixingRule</dictkey> in the <dict>transportProperties/</dict><subdict>transportModels</subdict> dictionary. The mixture shear viscosity and thermal conductivity can be printed by reproducing the procedure described in [§1.4](https://vincentcasseau.github.io/how-tos-cfd-transport/#14-print-species-shear-viscosity-and-thermal-conductivity)
  
```c++
    writeViscosityMixture          on;  
    writeThermalConducMixture      on; 
```

<br>

---

## 3) Mass diffusion

### 3.1 Disable multi-species diffusion
In the <dict>transportProperties/</dict><subdict>transportModels</subdict> dictionary, edit the following entries to
  
```c++
    multiSpeciesTransport         noSpeciesDiffusion;  
    binaryDiffusivityModel        noBinaryDiffusivityModel;
```
&nbsp;

### 3.2 Lewis number model
In the <dict>transportProperties/</dict><subdict>transportModels</subdict> dictionary, edit the following entries to 
 
```c++
    multiSpeciesTransport         LewisNumber;  
    binaryDiffusivityModel        noBinaryDiffusivityModel;
```

The Lewis number value can be found in the <subdict>diffusiveFluxesParameters</subdict> subdictionary.  

### 3.3 Fick's law and binary diffusion models
In the <dict>transportProperties/</dict><subdict>transportModels</subdict> dictionary, edit the following entries to
  
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

The <dictkey>constantBinaryDiffusivityModelCoefficients</dictkey> and <dictkey>yearGuptaModel</dictkey> entries can be found in the <subdict>diffusiveFluxesParameters</subdict> subdictionary. <dictkey>yearGuptaModel</dictkey> accepted values are <dictval>"1989"</dictval> or <dictval>"1990"</dictval>. Please refer to the <subdict>collisionData</subdict> dictionary for the correct combination.

Example:  

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

&nbsp;

### 3.4 SCEBD model 
In the <dict>transportProperties/</dict><subdict>transportModels</subdict> dictionary, edit the following entry to  

```c++
    multiSpeciesTransport         SCEBD; 
``` 

Please refer to [§3.3](https://vincentcasseau.github.io/how-tos-cfd-transport/#33-ficks-law-and-binary-diffusion-models) for the list of available binary diffusion coefficient models.

### 3.5 Additional features (to Fick and SCEBD models)
Results using the non-corrected forms of Fick's law and the SCEBD model can be obtained by switching on the <dictkey>useNonCorrectedForm</dictkey> boolean located in the <subdict>diffusiveFluxesParameters</subdict> subdictionary (for comparison with the corrected form only). It is turned to <dictval>off</dictval> by default, which means that the sum of the diffusive fluxes is zero.

> The <dictkey>useNonCorrectedForm</dictkey> entry can be deleted from the <subdict>diffusiveFluxesParameters</subdict> subdictionary if you wish (safer).

In the same subdictionary, the <dictkey>addPressureGradientTerm</dictkey> boolean adds on the effect of the pressure gradient.
