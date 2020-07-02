---
layout: page
title: How-tos
subtitle: CFD Module
nav-short: true
---

These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/genericCase).  

# Thermophysical modelling

---  
## 1) Species thermophysical properties

+ The species thermophysical properties are given in the [_thermoDEM_](https://github.com/vincentcasseau/hyStrath/blob/master/run/hyStrath/hy2Foam/genericCase/constant/thermoDEM) dictionary. For the nitrogen molecule, it is defined as follows:    
```c++
N2
{
    specie
    {
        nMoles          1;
        molWeight       28.0134;
        particleType    2;
        charge          0;
        diameter        4.17e-10;
        dissocEnergy    3.36e7;
        iHat            2.89e7;
        omega           0.74;
        eta_s           1.2;
        noVibTemp       1;
        noElecLevels    15; 
    }
    thermodynamics
    {
        decoupledCvCoeffs    ( 1.5 1 1 0 0 0 0 );
        vibrationalList      ( 1  3371 );
        electronicList       (  
                                1  0
                                3  7.223157e4
                                6  8.577863e4
                                6  8.605027e4
                                3  9.535119e4
                                1  9.805636e4
                                2  9.968268e4
                                2  1.048976e5
                                5  1.116490e5
                                1  1.225836e5
                                6  1.248857e5
                                6  1.282476e5
                                10 1.338061e5
                                6  1.404296e5
                                6  1.504959e5
                             );               
    }
    transport
    {}
}
```

In the _specie_ subdictionary, the molecular weight, _**molWeight**_, is given in g/mol.  
The subsequent entry named _**particleType**_ defines the particle type (0: electron, 1: neutral atom, 2: molecule, 3: charged molecule).  
Then, the keyword _**charge**_ indicates the charge of the particle (-1: electron, 0: neutral atom and molecule, +1: charged atom and molecule).  
Next comes the diameter of the particle, _**diameter**_, in meters.  
_**omega**_ is the temperature exponent of viscosity as described in [B. Transport](https://vincentcasseau.github.io/how-tos-cfd-transport/#13-other-transport-models). _**eta_s**_ is a factor that enters in the calculation of the [vibrational thermal conductivity](https://github.com/vincentcasseau/hyStrath/commit/f036d74297d3f91fcbeb05fa531a1c07ba71bde1) (this entry is optional and equal to 1.2 by default).
The number of vibrational energy modes of the particle is defined using the keyword _**noVibTemp**_ and finally the number of electronic energy levels is specified by the entry _**noElecLevels**_.
  
  
  
In the _thermodynamics_ subdictionary, the first entry is a list of coefficients called _**decoupledCvCoeffs()**_. The heat capacity at constant volume, _Cv_, is decomposed into the contributions of the different energy modes that are translational (element 1), rotational (element 2), vibrational (element 3), electronic (element 4), and electron (element 5). For a planar molecule,   
> Cv_t (T) = 1.5*R_m  

and  

> Cv_r (T) = 1.0*R_m 
 
where _R\_m_ is the specific gas constant. Thus, the first two elements in the _**decoupledCvCoeffs()**_ list are the coefficients by which _R\_m_ should be multiplied.

For the vibrational and electronic modes, the expressions of _Cv\_v_ and _Cv\_el_ are a function of the entries given in the following lists: _**vibrationalList()**_ and _**electronicList()**_. Hence, elements 3 and 4 can be seen as binary switches (see [§1.1](https://vincentcasseau.github.io/how-tos-cfd-thermophysical/#11-disablingenabling-the-vibrational-mode-of-a-molecule) and [§1.2](https://vincentcasseau.github.io/how-tos-cfd-thermophysical/#12-disablingenabling-the-electronic-mode-of-a-particle)).  

The 5th element of the list is the ratio of the species chemical enthalpy taken at 298 K (in J/mol) to the universal gas constant, while the 6th element is not used.  

Elements in the _**vibrationalList()**_ and _**electronicList()**_ lists are grouped by pairs with the first column being the degeneracy and the second column being the characteristic vibrational/electronic temperature (in K).  

### 1.1 Disabling/enabling the vibrational mode of a molecule 

In the _thermoDEM/#nameSpecies/thermodynamics_ dictionary, edit the 3rd element of the _**decoupledCvCoeffs**_ list to either be 0 (disabled) or 1 (enabled).  

In the following example, the vibrational energy mode of the N2 molecule is enabled  

```c++
        decoupledCvCoeffs    ( 1.5 1 1 0 0 0 0 );
```

### 1.2 Disabling/enabling the electronic mode of a particle  

In the _thermoDEM/#nameSpecies/thermodynamics_ dictionary, edit the 4th element of the _**decoupledCvCoeffs()**_ list to either be 0 (disabled) or 1 (enabled).  

In the following example, the electronic energy mode of the N atom is enabled  

```c++
        decoupledCvCoeffs    ( 1.5 0 0 1 0 56852 0 );
```
