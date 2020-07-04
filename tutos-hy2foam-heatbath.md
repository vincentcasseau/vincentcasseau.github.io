---
layout: page
title: Tutorials
nav-short: true
---
  
<p align="center">
  <img src="/docs/img/logos/hy2FoamLogo.png" width="210">
</p>

# Adiabatic heat bath

+ The working directory for the heat bath case is located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/heatBath).  

+ A description of the case scenario can be found in: V. Casseau _et al._, 10/2016: [A Two-Temperature Open-Source CFD Model for Hypersonic Reacting Flows, Part One: Zero-Dimensional Analysis](http://www.mdpi.com/2226-4310/3/4/34/html), Section _3.4. Relaxation of a Chemically-Reacting Mixture_.  

+ Running this tutorial:  

```sh
./Allclean  
./Allrun
```  

<br>

+ Solution: Time history for temperature and species number densities  

<p align="center">
  <img src="http://www.mdpi.com/aerospace/aerospace-03-00034/article_deploy/html/images/aerospace-03-00034-g007-550.jpg" width="400">
</p>

> _Influence of the chemistry-vibration model and chemical rate constants on a chemically-reacting N2−N heat bath. (a)Temperature versus time; (b)Normalised number density versus time._

<br>

+ Testing that the results are matching the solution:  

```sh
./Alltest
```  

<br>

---  

Contributor: Dr Vincent Casseau
