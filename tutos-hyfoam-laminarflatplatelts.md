<div class="paragraph"><p><br>
<br></p></div>
  
<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/hyFoamLogo.png" width="210">
</p>

# Mach 2 laminar flat plate (LTS)

+ The working directory for the 2D planar laminar flat plate is located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hyFoam/laminarFlatPlateLTS).  

+ An on-line description of the case scenario will soon be added.  

+ View of the mesh created using _blockMesh_    

<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-laminarFlatPlateLTS-mesh.png" width="400">
</p>


+ Running this tutorial:  
`./Allclean`  
`./Allrun`  

<div class="paragraph"><p><br>
<br></p></div>

+ Monitoring:   
`gnuplot gnuplot/monitorResiduals`    

<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-laminarFlatPlateLTS-residuals.png" width="400">
</p>

<div class="paragraph"><p><br>
<br></p></div>


+ Flow visualisations using Paraview:  

<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-laminarFlatPlateLTS-fieldTt.gif" width="600">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-laminarFlatPlateLTS-fieldMach.gif" width="600">  
</p>

<div class="paragraph"><p><br>
<br></p></div>

+ Post-processing:   
`gnuplot gnuplot/monitorCd`   
`gnuplot gnuplot/monitorIntegratedWallHeatFlux`  

<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-laminarFlatPlateLTS-dragCoefficient.png" width="450">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-laminarFlatPlateLTS-integratedWallHeatFlux.png" width="450">
</p>

<div class="paragraph"><p><br>
<br></p></div>

+ Solution: Sampling temperature, pressure, and velocity along a line normal to the plate and located at _x_ = 0.01 m away from the leading edge  

<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-laminarFlatPlateLTS-temperature.png" width="450">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-laminarFlatPlateLTS-pressure.png" width="450">  
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-laminarFlatPlateLTS-velocity.png" width="450">
</p>

> The small shift in normalised pressure is the result of having 2 distinct species (N2 and O2) as opposed to modelling air as being a single species.

<div class="paragraph"><p><br>
<br></p></div>

+ Testing that the results are matching the solution within a given tolerance:  
`./Alltest` 


<div class="paragraph"><p><br>
<br></p></div>


---  

##### Contributors: Dr Jimmy-John O.E. Hoste, Dr Daniel E.R. Espinoza, Dr Vincent Casseau