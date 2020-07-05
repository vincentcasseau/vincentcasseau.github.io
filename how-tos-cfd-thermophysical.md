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

The species thermophysical properties are given in the <dict>thermoDEM</dict> dictionary. For the nitrogen molecule, it is defined as follows
    
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

For the <subdict>specie</subdict> subdictionary, the Table below

<table>
  <tr>
    <td align="center" colspan="3"><b><subdict>specie</subdict> subdictionary</b></td>
  </tr>
  <tr>
    <td align="center"><b>Key</b></td>
    <td align="center"><b>Units</b></td>
    <td align="center"><b>Meaning</b></td>
  </tr>
  <tr>
    <td align="center"><dictkey>molWeight</dictkey></td>
    <td align="center"> g/mol </td>
    <td align="center">molecular weight</td>
  </tr>
  <tr>
    <td align="center"><dictkey>particleType</dictkey></td>
    <td align="center"> - </td>  
    <td align="center">type of particle (<dictval>0</dictval>: electron, <dictval>1</dictval>: neutral atom, <dictval>2</dictval>: molecule, <dictval>3</dictval>: charged molecule) </td>
  </tr>
  <tr>
    <td align="center"><dictkey>charge</dictkey></td>
    <td align="center"> - </td>  
    <td align="center">charge of the particle (<dictval>-1</dictval>: electron, <dictval>0</dictval>: neutral atom and molecule, <dictval>+1</dictval>: charged atom and molecule) </td>
  </tr>
  <tr>
    <td align="center"><dictkey>diameter</dictkey></td>
    <td align="center"> m </td>  
    <td align="center">diameter of the particle </td>
  </tr>
  <tr>
    <td align="center"><dictkey>omega</dictkey></td>
    <td align="center"> - </td>  
    <td align="center">temperature exponent of viscosity, see also: [B. Transport](https://vincentcasseau.github.io/how-tos-cfd-transport/#13-other-transport-models) </td>
  </tr>
  <tr>
    <td align="center"><dictkey>eta_s</dictkey></td>
    <td align="center"> - </td>  
    <td align="center">factor that enters in the calculation of the [vibrational thermal conductivity](https://github.com/vincentcasseau/hyStrath/commit/f036d74297d3f91fcbeb05fa531a1c07ba71bde1) (this entry is optional and equal to <dictval>1.2</dictval> by default) </td>
  </tr>
</table>


The number of vibrational energy modes of the particle is defined using the keyword <dictkey>noVibTemp</dictkey> and finally the number of electronic energy levels is specified by the entry <dictkey>noElecLevels</dictkey>.
  
  
  
In the <subdict>thermodynamics</subdict> subdictionary, the first entry is a list of coefficients called <dictkey>decoupledCvCoeffs()</dictkey>. The heat capacity at constant volume, _Cv_, is decomposed into the contributions of the different energy modes that are translational (element 1), rotational (element 2), vibrational (element 3), electronic (element 4), and electron (element 5). For a planar molecule,   
```
Cv_t (T) = 1.5*R_m 
``` 

and  

```
Cv_r (T) = 1.0*R_m 
```
 
where _R\_m_ is the specific gas constant. Thus, the first two elements in the <dictkey>decoupledCvCoeffs()</dictkey> list are the coefficients by which _R\_m_ should be multiplied.

For the vibrational and electronic modes, the expressions of _Cv\_v_ and _Cv\_el_ are a function of the entries given in the following lists: <dictkey>vibrationalList()</dictkey> and <dictkey>electronicList()</dictkey>. Hence, elements 3 and 4 can be seen as binary switches (see [§2.1](https://vincentcasseau.github.io/how-tos-cfd-thermophysical/#21-disablingenabling-the-vibrational-mode-of-a-molecule) and [§2.2](https://vincentcasseau.github.io/how-tos-cfd-thermophysical/#22-disablingenabling-the-electronic-mode-of-a-particle)).  

The 5th element of the list is the ratio of the species chemical enthalpy taken at 298 K (in J/mol) to the universal gas constant, while the 6th element is not used.  

Elements in the <dictkey>vibrationalList()</dictkey> and <dictkey>electronicList()</dictkey> lists are grouped by pairs with the first column being the degeneracy and the second column being the characteristic vibrational/electronic temperature (in K).  


&nbsp;

---  
## 2) Adding/removing energy modes

### 2.1 Disabling/enabling the vibrational mode of a molecule 

In the <dict>thermoDEM/</dict><subdict>#speciesName/thermodynamics</subdict> dictionary, edit the 3rd element of the <dictkey>decoupledCvCoeffs</dictkey> list to either be <dictval>0</dictval> (disabled) or <dictval>1</dictval> (enabled).  

In the following example, the vibrational energy mode of the N2 molecule is enabled  

```c++
        decoupledCvCoeffs    ( 1.5 1 1 0 0 0 0 );
```

&nbsp;

### 2.2 Disabling/enabling the electronic mode of a particle  

In the <dict>thermoDEM/</dict><subdict>#speciesName/thermodynamics</subdict> dictionary, edit the 4th element of the <dictkey>decoupledCvCoeffs()</dictkey> list to either be <dictval>0</dictval> (disabled) or <dictval>1</dictval> (enabled).  

In the following example, the electronic energy mode of the N atom is enabled  

```c++
        decoupledCvCoeffs    ( 1.5 0 0 1 0 56852 0 );
```
