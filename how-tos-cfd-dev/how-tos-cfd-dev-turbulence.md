---
layout: page
title: How-tos
subtitle: CFD Module
nav-short: true
---

These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/genericCase).  

# Turbulence modelling

---
## 1) Laminar flow simulation 
  
In the <dict>turbulenceProperties</dict> dictionary, edit the <dictkey>simulationType</dictkey> entry to <dictval>laminar</dictval>.

<br>

---
## 2) Turbulent flow simulation

In the <dict>turbulenceProperties</dict> dictionary, edit the <dictkey>simulationType</dictkey> entry to <dictval>RAS</dictval>.  
Then, in the <subdict>RAS</subdict> sub-dictionary, edit the <dictkey>RASModel</dictkey> to the desired turbulence model and the <dictkey>turbulence</dictkey> switch to <dictval>on</dictval>. Depending on which model is chosen, some fields may have to be added to the <dirname>0/</dirname> directory. Please refer to the official OpenFOAM tutorials for further information.

<br>
  
--- 

[**< D. Non-equilibrium flow modelling**](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev-nonequilibrium/)  
[**> F. MHD modelling**](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev-mhd/)  
[**&#x2191; Back to Contents**](https://vincentcasseau.github.io/how-tos-cfd-dev/how-tos-cfd-dev/)

