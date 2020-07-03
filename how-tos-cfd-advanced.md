---
layout: page
title: How-tos
subtitle: CFD Module
nav-short: true
---

These how-tos are based on the working folder located [here](https://github.com/vincentcasseau/hyStrath/tree/master/run/hyStrath/hy2Foam/genericCase).  

# Advanced features

---  
## 1) Local time stepping
  
In the <dirname>system/</dirname> directory, open the <dict>fvSchemes</dict> dictionary and edit the default <dictkey>ddtSchemes</dictkey> entry to <dictval>localEuler rDeltaT</dictval>.

> Local time stepping is currently inappropriate for axisymmetric and chemically-reacting simulations.  

The [Lorrain scramjet tutorial](https://vincentcasseau.github.io/tutos-hyfoam/#3-lorrain-geometry) is a suitable case for running LTS and the aforementioned time discretisation scheme is the only modification to be made.

<br>

---  
## 2) On-the-fly dictionary editing  

On-the-fly editing was made available primarily for computations on a high-performance computer on which days can be lost waiting in a priority queue. The different steps to follow are explained below depending on the dictionary that is affected by the changes.

For the <strong><dict>transportProperties</dict> dictionary</strong>:  
  + Open the <dict>transportProperties</dict> dictionary  
  + Edit one or several entries inside the <subdict>rarefiedParameters</subdict> or <subdict>transportModels</subdict> subdictionaries  
  + [NB: if you save the file at this point, nothing will happen] 
  + Add an entry to the modified subdictionary that is: _**applyChanges        true;**_
  + Save the file  
  + [For safety, once the modification has taken effect, the file can be re-opened and the <dictkey>applyChanges</dictkey> entry can be removed. Save again.]  
  + If this operation has worked, then your simulation should have entered into a second sub-phase of the run as shown in the log file

Before:  

```c++
Phase no 1.0  ExecutionTime = 72.29 s  ClockTime = 74 s  Iteration no 4504 (0.04 s)
```

After:

```c++
Phase no 1.1  ExecutionTime = 72.32 s  ClockTime = 74 s  Iteration no 4505 (0.03 s)
```

For the <strong><dict>thermo2TModel</dict> dictionary<strong>:  
    - The steps are equivalent to the <dict>transportProperties</dict> dictionary: add the entry _**applyChanges        true;**_ after editing the desired subdictionary and save.  


For **any other dictionary**:
    - Make modifications to the dictionary in question (_e.g._, adding extra chemical reaction, etc) and save.  
    - Open the <dict>hTCProperties</dict> dictionary and add the entry: _**applyChanges        true;**_  
    - Save the <dict>hTCProperties</dict> dictionary  

As shown in the log file, the simulation enters into a new stage/phase

Before:  

```c++
Phase no 1.1  ExecutionTime = 153.02 s  ClockTime = 157 s  Iteration no 9074 (0.03 s)
```

After:

```c++
Phase no 2.0  ExecutionTime = 153.05 s  ClockTime = 157 s  Iteration no 9075 (0.03 s)
```

> NB: For all dictionaries, _**applyChangesAtWriteTime        true;**_ can be used instead of _**applyChanges        true;**_ in case the solution needs to be printed before applying modification(s) to the computation.  

<br>

For **boundary conditions**:  
    - Open the <dict>hTCProperties</dict> dictionary   
    - Add the entry _**applyChangesAtWriteTimeAndWait        #numberOfSeconds;**_ where _**#numberOfSeconds**_ is an integer value prescribing the time during which the simulation will be paused.  
    - Save the <dict>hTCProperties</dict> dictionary   
    - Type in: _tail -f log.hy2Foam_ into the terminal window and wait until the next write time  
    - Once the simulation is sleeping, _reconstructPar_ can be used (for a parallel job)  
    - Edit the desired boundary condition and save  
    - Delete the _processors#ID_ folders and run: _decomposePar -latestTime_ 
    - Monitor the log file as the simulation restarts to make sure everything went well  

<br>

---  
## 3) Bounding the temperature field

Within the <dict>thermophysicalProperties</dict> dictionary, the <subdict>temperatureBounds</subdict> subdictionary can be copy-pasted to bound the temperature field and increase robustness. After stopping the simulation, please make sure that the minimum and maximum temperature values are strictly within these bounds.

```c++
temperatureBounds
{
    Tlow      200; //default is   100 K
    Thigh   40000; //default is 40000 K
}
```

If the temperature field goes unbounded, a warning will be printed in the log file for this iteration. It tells the number of times the _limit_ function had to be called and the minimum/maximum temperature recorded before bounding.

```c++
Attempt to use rho2ReactionThermo out of temperature range 3197 times during this iteration.
		Thigh: 40000 < 45289
```

<br>

---  
## 4) The _hyLight_ switch

The <dictkey>hyLight</dictkey> switch located into the <dict>thermophysicalProperties</dict> dictionary disables some of the code features to run a minimalistic version of the solver. For instance, quantities like the Knudsen number or the overall temperature will not be calculated at each time-step when this boolean is switched <dictkey>on</dictkey> (even when the set-up of the <dict>transportProperties</dict> dictionary is telling otherwise). The solution should not be affected by the state of the <dictkey>hyLight</dictkey> switch, only the number of fields to be printed might differ.
