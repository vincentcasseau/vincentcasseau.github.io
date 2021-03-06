---
layout: page
title: Tutorials
nav-short: true
---
  
<p align="center">
  <img src="/docs/img/logos/hyFoamLogo.png" width="210">
</p>

# Mach 2 laminar flat plate (LTS)

+ The working directory for the 2D planar laminar flat plate is located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hyFoam/laminarFlatPlateLTS).  

+ View of the mesh created using _blockMesh_    

<p align="center">
<img src="/docs/img/tutos/hyFoam/tutorial-laminarFlatPlateLTS-mesh.png" width="400">
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

<p align="center">
<img src="/docs/img/tutos/hyFoam/tutorial-laminarFlatPlateLTS-residuals.png" width="400">
</p>

<br>

+ Flow visualisations using Paraview:  

<p align="center">
<img src="/docs/img/tutos/hyFoam/tutorial-laminarFlatPlateLTS-fieldTt.gif" width="600">
<img src="/docs/img/tutos/hyFoam/tutorial-laminarFlatPlateLTS-fieldMach.gif" width="600">  
</p>

<br>

+ Post-processing:   

```sh
gnuplot gnuplot/monitorCd   
gnuplot gnuplot/monitorIntegratedWallHeatFlux  
```

<p align="center">
<img src="/docs/img/tutos/hyFoam/tutorial-laminarFlatPlateLTS-dragCoefficient.png" width="450">
<img src="/docs/img/tutos/hyFoam/tutorial-laminarFlatPlateLTS-integratedWallHeatFlux.png" width="450">
</p>

<br>

+ Solution: Sampling temperature, pressure, and velocity along a line normal to the plate and located at _x_ = 0.01 m away from the leading edge  

<p align="center">
<img src="/docs/img/tutos/hyFoam/tutorial-laminarFlatPlateLTS-temperature.png" width="450">
<img src="/docs/img/tutos/hyFoam/tutorial-laminarFlatPlateLTS-pressure.png" width="450">  
<img src="/docs/img/tutos/hyFoam/tutorial-laminarFlatPlateLTS-velocity.png" width="450">
</p>

> The small shift in normalised pressure is the result of having 2 distinct species (N2 and O2) as opposed to modelling air as being a single species.

<br>

+ Testing that the results are matching the solution within a given tolerance:  
```sh
./Alltest
``` 

<br>

---  

Contributors: Dr Jimmy-John O.E. Hoste, Dr Daniel E.R. Espinoza, Dr Vincent Casseau
