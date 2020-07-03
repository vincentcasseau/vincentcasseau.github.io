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

+ In the <dict>turbulenceProperties</dict> dictionary, edit the <dictkey>simulationType</dictkey> entry to <dictval>RAS</dictval>  
+ In the <dict>turbulenceProperties</dict> dictionary, <subdict>RAS</subdict> sub-dictionary, edit the <dictkey>RASModel</dictkey> entry to the desired turbulence model and the <dictkey>turbulence</dictkey> switch to <dictval>on</dictval>.
+ Depending on which model is chosen, some fields may have to be added to the <dirname>0/</dirname> directory.

