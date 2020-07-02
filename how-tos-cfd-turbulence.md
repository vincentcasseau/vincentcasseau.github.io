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
  
+ In the _turbulenceProperties_ dictionary, edit the _simulationType_ entry to __*laminar*__

<div class="paragraph"><p><br>
<br></p></div>

---

## 2) Turbulent flow simulation

+ In the _turbulenceProperties_ dictionary, edit the _simulationType_ entry to __*RAS*__  
+ In the _turbulenceProperties_ dictionary, __*RAS*__ sub-dictionary, edit the _RASModel_ entry to the desired turbulence model and the _turbulence_ switch to __*on*__

+ Depending on which model is chosen, some fields may have to be added to the _0/_ directory.


<div class="paragraph"><p><br>
<br></p></div>

---

Contributor: Dr Vincent Casseau

