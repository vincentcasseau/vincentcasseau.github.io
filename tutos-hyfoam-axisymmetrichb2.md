---
layout: page
title: Tutorials
nav-short: true
---
  
<p align="center">
  <img src="/docs/img/logos/hyFoamLogo.png" width="210">
</p>

# Mach 9.59 HB2 configuration  

+ The working directory for the ogive-cylinder-flare HB2 configuration is located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hyFoam/axisymmetric-HB2).
+ Views of the mesh (entire domain and zoomed in on the nose region)

<p align="center">
<img src="/docs/img/tutos/hyFoam/tutorial-axisymmetricHB2-meshFull.png" width="400"><img src="/docs/img/tutos/hyFoam/tutorial-axisymmetricHB2-meshNose.png" width="370">
</p>


+ Running this tutorial:  
```sh
./Allclean  
./Allrun
```

<br>

+ Monitoring:   
```sh
gnuplot gnuplot/monitorResiduals
```   

<br>

+ Flow visualisations using Paraview:  

<p align="center">
<img src="/docs/img/tutos/hyFoam/tutorial-axisymmetricHB2-fieldMach.png" width="600">
<img src="/docs/img/tutos/hyFoam/tutorial-axisymmetricHB2-fieldTt.png" width="600">
</p>

<br>

+ Post-processing: 
```sh
gnuplot gnuplot/monitorCd
gnuplot gnuplot/monitorIntegratedWallHeatFlux
```  

<br>

+ Solution: wall heat flux along the HB2 surface

<p align="center">
<img src="/docs/img/tutos/hyFoam/tutorial-axisymmetricHB2-wallHeatFlux.png" width="550">
</p>

<br>

---  

Contributors: Dr Jimmy-John O.E. Hoste, Dr Daniel E.R. Espinoza, Dr Vincent Casseau
