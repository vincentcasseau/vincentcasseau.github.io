---
layout: page
title: How-tos
subtitle: CFD Module
nav-short: true
---

These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/genericCase).  

# Monitoring & Post-processing

---  
## 1) Monitoring 

### 1.1 Wall heat flux  

Pre-requirement: the patch type in <dirname>constant/polyMesh/</dirname><dict>boundary</dict> has to be <dictval>wall</dictval>.  

Open the <dict>transportProperties</dict> dictionary and make sure the switch is active  

```c++
    writeWallHeatFlux              on;
```

The field named _wallHeatFlux_ will be printed as a result in each time folder. In addition, the wall heat flux is integrated for each wall and printed in the log file at write time

```c++
Wall heat fluxes [W]
Patch 4 named lowerWall: 416.2644537
```

Thus, the integrated wall heat flux can easily be monitored (and later plotted) during the simulation using the _grep_ command. In the present case

```sh
grep lowerWall log.hy2Foam
```

Alternatively, use the dedicated monitoring script given in the <dirname>gnuplot/</dirname> folder, called _monitorIntegratedWallHeatFlux_, and replace _#patchName_ by the name of the wall patch.  

```c++
set output "gnuplot/integratedWallHeatFlux.eps"

set size 0.95,0.47
set origin 0.03,0.53
set xlabel "Time  [sec]"
set ylabel "Integrated wall heat flux  [kW]"

plot \
"< cat log.hy2Foam | grep -e 'named #patchName:' -e '^Time =' | awk '/^Time =/,/^Time =/ {lastc = $0; next}{ if ( lastc != \"\") { print lastc; lastc = \"\"; } print }' $1 | cut -d ':' -f 2 | cut -d '=' -f 2 | paste -d ' ' - -" u 1:($2/1000.0) w l ls 1 lw 1.8 not
```

&nbsp;

### 1.2 Wall shear stress

In the <dirname>system/</dirname><dict>controlDict</dict> dictionary, uncomment the include statement that prints surface quantities 
  
```c++
functions
{
    //#include "probes"
    
    //#include "forces"

    #include "surfaceQuantities"
}
```

and review/edit the relevant subdictionary in the <dirname>system/</dirname><dict>surfaceQuantities</dict> dictionary

```c++
wallShearStress
{
    type            wallShearStress;
    libs            ("libstrathFieldFunctionObjects.so");
    patches         ("cylinder");
    writeControl    outputTime;
    log             no;
}
```

&nbsp;

### 1.3 Forces

In the <dirname>system/</dirname><dict>controlDict</dict> dictionary, uncomment the include statement that prints forces and aerodynamic coefficients
  
```c++
functions
{
    //#include "probes"
    
    #include "forces"

    //#include "surfaceQuantities"
}
```

Open the <dirname>system/</dirname><dict>forces</dict> dictionary  

```c++
#include "../0/include/initialConditions"

forces
{
    type forces;
    functionObjectLibs ("libstrathForces.so");
    log false;
    writeFields false;
    patches (cylinder); // edit accordingly
    CofR (0 0 0);
    dragDir (1 0 0);
    liftDir (0 1 0);
    pitchAxis (0 0 1);
}

forceCoeffs
{
    #include "../0/include/initialConditions"

    type forceCoeffs;
    functionObjectLibs ("libstrathForces.so");
    log false;
    writeFields false;
    patches (cylinder); // edit accordingly
    rho rhoInf;
    rhoInf $rhoInlet;
    magUInf $velocityInlet;
    CofR (0 0 0);
    dragDir (1 0 0);
    liftDir (0 1 0);
    pitchAxis (0 0 1);
    lRef 0.05; // edit accordingly, see constant/transportProperties/rarefiedParameters/characteristicLength
    Aref 1.96646e-05; // edit accordingly
}
```

Review and edit the relevant entries. Forces / aerodynamic coefficients (_e.g._ drag coefficient) can be monitored using the script file given in the <dirname>gnuplot/</dirname> folder
  
```c++
set output "gnuplot/dragCoefficient.eps"

set size 0.95,0.47
set origin 0.03,0.53
set xlabel "Write time"
set ylabel "Drag coefficient"

plot \
"< cat log.hy2Foam | grep 'Cd' | cut -d '=' -f 2" w l ls 1 not
```

&nbsp;

### 1.4 Residuals

An example is given below for monitoring the residuals. The fields (_**Ux**_, _**Uy**_, _**e\_{ve, N2}**_, _**e**_) may be edited depending on the simulation set-up.

```sh
set output "gnuplot/residuals.eps"

set size 0.95,0.47
set origin 0.03,0.53
set logscale y
set format y "10^{\%01T}"
set xlabel "Timestep [x 100]"
set ylabel "Residuals"
set mytics 10

plot \
"< cat log.hy2Foam | grep 'Solving for Ux' | cut -d '=' -f 2 | cut -d ',' -f 1" every 100 w l ls 12 t 'Ux initial',\
"< cat log.hy2Foam | grep 'Solving for Ux' | cut -d '=' -f 3 | cut -d ',' -f 1" every 100 w l ls 1  t 'Ux final',\
"< cat log.hy2Foam | grep 'Solving for Uy' | cut -d '=' -f 2 | cut -d ',' -f 1" every 100 w l ls 22 t 'Uy initial',\
"< cat log.hy2Foam | grep 'Solving for Uy' | cut -d '=' -f 3 | cut -d ',' -f 1" every 100 w l ls 2 t 'Uy final',\
"< cat log.hy2Foam | grep 'Solving for evel_N2' | cut -d '=' -f 2 | cut -d ',' -f 1" every 100 w l ls 32 t 'e_{vel,{N_2}} initial',\
"< cat log.hy2Foam | grep 'Solving for evel_N2' | cut -d '=' -f 3 | cut -d ',' -f 1" every 100 w l ls 3 t 'e_{vel,{N_2}} final',\
"< cat log.hy2Foam | grep 'Solving for e,' | cut -d '=' -f 2 | cut -d ',' -f 1" every 100 w l ls 42 t 'e initial',\
"< cat log.hy2Foam | grep 'Solving for e,' | cut -d '=' -f 3 | cut -d ',' -f 1" every 100 w l ls 4 t 'e final'
```

and this script can be run as follows

```c++
gnuplot gnuplot/monitorResiduals
```

<br>

---  
## 2) Post-processing

In a terminal window, type in
  
```c++
hy2Foam -postProcess -dict 'system/surfaceCoefficients' -latestTime
``` 
 
where <dirname>system/</dirname><dict>surfaceCoefficients</dict> is a dictionary that contains the desired surface coefficients. Their implementation in the <subdict>functions</subdict> sub-dictionary is shown below.

### 2.1 Pressure coefficient

In the <subdict>functions</subdict> sub-dictionary, add  
  
```c++
pressureCoefficient
{
    type            pressureCoefficient;
    libs            ("libstrathFieldFunctionObjects.so");
    writeControl    outputTime;
    log             no;
}
```

&nbsp;

### 2.2 Stanton number

The _**wallHeatFlux**_ field is a required input.
In the <subdict>functions</subdict> sub-dictionary, add
  
```c++
StantonNumber
{
    type            StantonNo;
    //- see constant/transportProperties/transportModels: writeWallHeatFlux
    wallHeatFlux    "wallHeatFlux"; 
    libs            ("libstrathFieldFunctionObjects.so");
    writeControl    outputTime;
    log             no;
}
```

&nbsp;

### 2.3 Skin-friction coefficient

The _**wallShearStress**_ field is a required input.
In the <subdict>functions</subdict> sub-dictionary, add  
  
```c++
frictionCoefficient
{
    type            frictionCoefficient;
    libs            ("libstrathFieldFunctionObjects.so");
    writeControl    outputTime;
    log             no;
}
```

&nbsp;

### 2.4 y+

In the <subdict>functions</subdict> sub-dictionary, add  

```c++
yPlus
{
    type            yPlus;
    libs            ("libstrathFieldFunctionObjects.so");
    writeControl    outputTime;
    log             no;
}
```

&nbsp;

### 2.5 ParaView

+ Open ParaView and load wall patches in _Mesh Regions_  
+ Plot any of these surface quantities using the _**plotData**_ filter
