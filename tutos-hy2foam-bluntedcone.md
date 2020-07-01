<div class="paragraph"><p><br>
<br></p></div>
  
<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/hy2FoamLogo.png" width="210">
</p>

# Blunted cone

+ The working directory for the 2D axisymmetric blunted cone is located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/bluntedCone).  

+ A description of the case scenario can be found in: V. Casseau _et al._, 12/2016: [A Two-Temperature Open-Source CFD Model for Hypersonic Reacting Flows, Part Two: Multi-Dimensional Analysis](http://www.mdpi.com/2226-4310/3/4/45/html), Section _3.1. Mach 11.3 Blunted Cone_.  

+ View of the _gmsh_ mesh provided in the _constant/backup-polyMesh_ folder  

<p align="center">
<img src="http://www.mdpi.com/aerospace/aerospace-03-00045/article_deploy/html/images/aerospace-03-00045-g001.png" width="400">
</p>

> _Mesh for the blunted cone (each 5th line is represented in each direction)._

+ Running this tutorial:  
`./Allclean`  
`./Allrun`  

<div class="paragraph"><p><br>
<br></p></div>

+ Monitoring:   
`gnuplot gnuplot/monitorResiduals`    

<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hy2Foam/tutorial-bluntedCone-residuals.png" width="400">
</p>

<div class="paragraph"><p><br>
<br></p></div>


+ Flow visualisations using Paraview:  

<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hy2Foam/tutorial-bluntedCone-fieldTt.gif" width="500">  
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hy2Foam/tutorial-bluntedCone-fieldTv.gif" width="500">  
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hy2Foam/tutorial-bluntedCone-fieldMach.gif" width="500">  
</p>

<div class="paragraph"><p><br>
<br></p></div>

+ Post-processing:   
`gnuplot gnuplot/monitorCd`   
`gnuplot gnuplot/monitorIntegratedWallHeatFlux`  

<p align="center">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hy2Foam/tutorial-bluntedCone-dragCoefficient.png" width="400">
<img src="https://github.com/vincentcasseau/hyStrath/blob/master/doc/images/tutorials/hy2Foam/tutorial-bluntedCone-integratedWallHeatFlux.png" width="400">
</p>

+ Solution: stagnation line data and surface coefficients
<p align="center">
<img src="http://www.mdpi.com/aerospace/aerospace-03-00045/article_deploy/html/images/aerospace-03-00045-g002.png" width="800">
</p>

> _(a–c) Stagnation line profiles, and (d–f) surface quantities along the blunted cone; (a) normalised temperature; (b) normalised mass density; (c) normalised velocity; (d) pressure coefficient; (e) friction coefficient; (f) Stanton number._

<div class="paragraph"><p><br>
<br></p></div>

+ Testing that the results are matching the solution within a given tolerance:  
`./Alltest`  

<div class="paragraph"><p><br>
<br></p></div>

---  

##### Contributors: Dr Vincent Casseau and Dr Daniel E.R. Espinoza