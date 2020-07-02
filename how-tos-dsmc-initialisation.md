---
layout: page
title: How-tos
subtitle: DSMC Module
---

# Initialisation

<br>

---
## 1) Creating the _0/_ folder
{: #1-creating-the-0-folder} 
 
In the working directory, type in:  
```sh
dsmcInitialise+
```
This command line will create the _0/_ folder. Simulators data is stored into the _0/lagrangian/dsmc/_ subfolder and two volume fields, _cellLevel_ and _dsmcSigmaTcRMax_, are printed. The main DSMC executable will always look for these information in the time folder corresponding to the starting time. 

## 2) Simulators data  
{: #2-simulators-data }

| File    | Meaning          |
|:-------------:|-------------|
| _positions_      | positions in Cartesian space |
| _U_      | velocity vector |
| _typeId_ | species index, cf. species list given in the _dsmcProperties_ dictionary |
| _newParcel_      | -1 if seeded at t = 0 or index of the patch the simulator entered the domain |
| _origProcId_ | index of the processor dealing with the simulator |
| _origId_ | local particle index in processor _origProcId_ |
| _classification_      | not used, to be revised |
|   |  |
| ERot      | rotational energy |
| vibLevel      | vibrational energy level for each vibrational energy mode |
| ELevel      | electronic energy level |

## 3) Initial volume fields 
{: #3-initial-volume-fields }
 
+ _dsmcSigmaTcRMax_ is a first estimate of the maximum value taken by the product of the collision cross-section by the relative speed. For a gas mixture, it is usually obtained by considering the properties (diameter, omega, alpha) of the most abundant species. As the simulation proceeds, this field is updated as soon as a new local maximum is found. It requires no user intervention.

+ _cellLevel_ represents the level of refinement of each cell. At _t_ = 0, it is equal to 0 which means that all cells are root cells (they cannot be further coarsened). This field will only be used when the AMR flag is passed as an argument to the main DSMC executable.

<br>

---

Contributor: Dr Vincent Casseau
