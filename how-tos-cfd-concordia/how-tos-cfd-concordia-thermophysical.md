---
layout: page
title: How-tos
subtitle: CFD Module - Concordia release
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

The Table below lists the meaning of the different keys present in the <subdict>specie</subdict> subdictionary. 

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
    <td align="center"><dictkey>nMoles</dictkey></td>
    <td align="center"> - </td>
    <td align="center">deprecated OpenFOAM entry, always set to <dictval>1</dictval></td>
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
    <td align="center">temperature exponent of viscosity, see also: <a href="https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordiatransport/#13-other-transport-models">B. Transport</a></td>
  </tr>
  <tr>
    <td align="center"><dictkey>eta_s</dictkey></td>
    <td align="center"> - </td>  
    <td align="center">factor that enters in the calculation of the <a href="https://github.com/vincentcasseau/hyStrath/commit/f036d74297d3f91fcbeb05fa531a1c07ba71bde1">vibrational thermal conductivity</a> (this key is optional and is equal to <dictval>1.2</dictval> by default) </td>
  </tr>
  <tr>
    <td align="center"><dictkey>noVibTemp</dictkey></td>
    <td align="center"> - </td>  
    <td align="center"> number of vibrational energy modes </td>
  </tr>
  <tr>
    <td align="center"><dictkey>noElecLevels</dictkey></td>
    <td align="center"> - </td>  
    <td align="center"> number of electronic energy levels </td>
  </tr>
  <tr>
    <td align="center"><dictkey>dissocEnergy</dictkey></td>
    <td align="center"> J/kg </td>  
    <td align="center"> species dissociation potential, used in the <a href="https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordianonequilibrium/#411-general-settings">preferential model</a> </td>
  </tr>
  <tr>
    <td align="center"><dictkey>iHat</dictkey></td>
    <td align="center"> n/a </td>  
    <td align="center"> under development</td>
  </tr>
</table>

In the <subdict>thermodynamics</subdict> subdictionary, the first entry is a list of coefficients called <dictkey>decoupledCvCoeffs()</dictkey>. The heat capacity at constant volume, _Cv_, is decomposed into the contributions of the different energy modes that are translational (element 1), rotational (element 2), vibrational (element 3), electronic (element 4), and electron (element 5). For a planar molecule,   
<p>
$$Cv_t = 1.5*R_m$$
</p>
<p>and</p>
<p>
$$Cv_r = 1.0*R_m$$
</p>
 
<p>where `R_m` is the specific gas constant. Thus, the first two elements in the <dictkey>decoupledCvCoeffs()</dictkey> list are the coefficients by which `R_m` should be multiplied.</p>

<p>For the vibrational and electronic modes, the expressions of `Cv_v` and `Cv_{el}` are a function of the valus provided in the <dictkey>vibrationalList()</dictkey> and <dictkey>electronicList()</dictkey> lists. Hence, elements 3 and 4 can be seen as switches (see <a href="https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordiathermophysical/#21-disablingenabling-the-vibrational-mode-of-a-molecule">§2.1</a> and <a href="https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordiathermophysical/#22-disablingenabling-the-electronic-mode-of-a-particle">§2.2</a>). Elements in the <dictkey>vibrationalList()</dictkey> and <dictkey>electronicList()</dictkey> lists are grouped by pairs with the first column being the degeneracy and the second column being the characteristic vibrational/electronic temperature, in Kelvins.</p>   

The 5th element of the <dictkey>decoupledCvCoeffs()</dictkey> list is the ratio of the species chemical enthalpy taken at 298 K (in J/mol) to the universal gas constant, while the 6th element is not used.  

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

<br>
  
--- 

[**> B. Transport modelling**](https://vincentcasseau.github.io/how-tos-cfd-concordia/how-tos-cfd-concordiatransport/)  
[**&#x2191; Back to Contents**](https://vincentcasseau.github.io/how-tos-cfd/)
