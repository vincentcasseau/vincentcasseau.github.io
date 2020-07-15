---
layout: page
title: How-tos
subtitle: CFD Module
nav-short: true
---

These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/genericCase).  

# Transport modelling

---
## 1) Species shear viscosity and thermal conductivity

### 1.1 Inviscid simulation    

This is done in two steps:  
  + in the <dict>thermophysicalProperties/</dict><subdict>thermoType</subdict> dictionary, edit the <dictkey>transport</dictkey> entry to <dictval>constant</dictval>;
  + in the <dict>thermoDEM/</dict><subdict>#speciesName/transport/constant</subdict> dictionary, for all species present in the gas mixture, edit the value of the entry <dictkey>mu</dictkey> to be <dictval>0</dictval>.

### 1.2 Viscous simulation with constant shear viscosity and thermal conductivity

Repeat the two steps presented in [§1.1](https://vincentcasseau.github.io/how-tos-cfd-transport/#11-inviscid-simulation) but edit <dictkey>mu</dictkey> to the desired value. The thermal conductivity is then calculated using Eucken's formula.

### 1.3 Other transport models

The names of all other available transport models to be loaded using the <dictkey>transport</dictkey> keyword in the <dict>thermophysicalProperties/</dict><subdict>thermoType</subdict> dictionary are  

| Transport model name    | Parameters          |
|:-------------:|-------------|
| <dictval>SutherlandEucken</dictval>      | <dictkey>As</dictkey>, <dictkey>Ts</dictkey>     |
| <dictval>BlottnerEucken</dictval> | <dictkey>A</dictkey>, <dictkey>B</dictkey>, <dictkey>C</dictkey>     |
| <dictval>CEA</dictval>      | <dictkey>temp()</dictkey>, <dictkey>visco()</dictkey>, <dictkey>kappa()</dictkey>      |
| <dictval>powerLawEucken</dictval> | <dictkey>diameter</dictkey>, <dictkey>omega</dictkey>     |

The coefficients of these models can be found in the <dict>thermoDEM/</dict><subdict>#speciesName</subdict> dictionary. The first three models are using coefficients located in the <subdict>transport</subdict> subdictionary, while the <dictval>powerLawEucken</dictval> model requires the species diameter, <dictkey>diameter</dictkey>, and the species temperature exponent of viscosity, <dictkey>omega</dictkey>, located in the <subdict>specie</subdict> subdictionary.

### 1.4 Print species shear viscosity and thermal conductivity
In the <dict>transportProperties/</dict><subdict>transportModels</subdict> dictionary, edit any of these two switches to <dictval>on</dictval>  

```c++
    writeViscositySpecies          on;  
    writeThermalConducSpecies      on; 
```

<br>

---
## 2) Mixing rules

The available mixing rules are given in the following Table 

| Mixing rule name    | Parameters          |
|:-------------:|:-------------:|
| <dictval>molar</dictval>      | - |
| <dictval>Wilke</dictval>      | - |
| <dictval>ArmalySutton</dictval> | <dictkey>correctedArmalySutton</dictkey>    |

and the dedicated entry, <dictkey>mixingRule</dictkey>, is located in the <dict>transportProperties/</dict><subdict>transportModels</subdict> dictionary. The mixture shear viscosity and thermal conductivity can be printed by switching <dictval>on</dictval> the following booleans
  
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

The Lewis number value can be found in the <subdict>diffusiveFluxesParameters</subdict> subdictionary

```c++
    diffusiveFluxesParameters
    {
        LewisNumber                    1.4;
        
        [...]
    }
``` 

&nbsp; 

### 3.3 Fick's law and binary diffusion models
In the <dict>transportProperties/</dict><subdict>transportModels</subdict> dictionary, edit the following entry to
  
```c++
    multiSpeciesTransport         Fick; 
``` 

Binary diffusion coefficients can be calculated according to any of the models presented in the Table below  

| Binary diffusion model name    | Parameters          |
|:-------------:|-------------|
| <dictval>constant</dictval>      | <dictkey>constantBinaryDiffusivityModelCoefficients</dictkey> |
| <dictval>collisionData</dictval>      | <dictkey>collisionDataModel</dictkey>, <subdict>collisionData</subdict> dict     |
| <dictval>Stephani</dictval> | <dictkey>molWeight</dictkey>, <dictkey>diameter</dictkey>, <dictkey>omega</dictkey>     |

The <dictkey>constantBinaryDiffusivityModelCoefficients</dictkey> and <dictkey>collisionDataModel</dictkey> entries can be found in the <subdict>diffusiveFluxesParameters</subdict> subdictionary. <dictkey>collisionDataModel</dictkey> accepted values are <dictval>"Gupta1989D"</dictval>, <dictval>"Gupta1989O"</dictval>, <dictval>"Gupta1990D"</dictval>, <dictval>"Gupta1990O"</dictval>, and <dictval>"Wright2005O"</dictval>.

Example:  

```c++
multiSpeciesTransport        Fick;
binaryDiffusivityModel       collisionData;  
  
diffusiveFluxesParameters   
{  
     collisionDataModel          "Gupta1989D";   
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
Results using the non-corrected forms of Fick's law and the SCEBD model can be obtained by switching on the <dictkey>useNonCorrectedForm</dictkey> boolean located in the <subdict>diffusiveFluxesParameters</subdict> subdictionary (for comparison with the corrected form only). It is turned <dictval>off</dictval> by default, which means that the sum of the diffusive fluxes is zero.

> The <dictkey>useNonCorrectedForm</dictkey> entry can be deleted from the <subdict>diffusiveFluxesParameters</subdict> subdictionary if you wish (safer).

In the same subdictionary, the <dictkey>addPressureGradientTerm</dictkey> switch allows to account for the effects of pressure gradients.
