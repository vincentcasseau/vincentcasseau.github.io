<div class="paragraph"><p><br>
<br></p></div>
  
<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/hyFoamLogo.png" width="210">
</p>

# Mach 9.59 HB2 configuration  

+ The working directory for the ogive-cylinder-flare HB2 configuration is located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hyFoam/axisymmetric-HB2).  

+ An on-line description of the case scenario will soon be added.  

+ Views of the mesh (entire domain and zoomed in on the nose region)

<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-axisymmetricHB2-meshFull.png" width="400"><img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-axisymmetricHB2-meshNose.png" width="370">
</p>


+ Running this tutorial:  
`./Allclean`  
`./Allrun`  

<div class="paragraph"><p><br>
<br></p></div>

+ Monitoring:   
`gnuplot gnuplot/monitorResiduals`    


<div class="paragraph"><p><br>
<br></p></div>


+ Flow visualisations using Paraview:  

<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-axisymmetricHB2-fieldMach.png" width="600">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-axisymmetricHB2-fieldTt.png" width="600">
</p>

<div class="paragraph"><p><br>
<br></p></div>

+ Post-processing:   
`gnuplot gnuplot/monitorCd`   
`gnuplot gnuplot/monitorIntegratedWallHeatFlux`  

> Results are given in the _gnuplot/solution_ folder.

<div class="paragraph"><p><br>
<br></p></div>

+ Solution: wall heat flux along the HB2 surface

<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hyFoam/tutorial-axisymmetricHB2-wallHeatFlux.png" width="550">
</p>

<div class="paragraph"><p><br>
<br></p></div>


---  

##### Contributors: Dr Jimmy-John O.E. Hoste, Dr Daniel E.R. Espinoza, Dr Vincent Casseau