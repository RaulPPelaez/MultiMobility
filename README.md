## MultiMobility
A library with C++ and Python interfaces to compute the hydrodynamic displacements of a group of particles (blobs) at the RPY level due to a series of forces acting on them. Both the deterministic and stochastich displacements can be requested.  
This repo is a common interface to other tools already available in my other repositories. In particular, this repo computes the mobility in the following geometries:  
  * Open boundaries (direct N^2 evaluation of the RPY tensor), see [](https://github.com/RaulPPelaez/BatchedNBodyRPY).  
  * Triply Periodic (using PSE), see [](https://github.com/RaulPPelaez/UAMMD_PSE_Python).  
  * Doubly Periodic (using DPStokes), see [](https://github.com/stochasticHydroTools/DoublyPeriodicStokes).  

### Dependencies
All the tools are GPU enabled using CUDA, thus requiring a working CUDA installation.  
Lapacke+cblas (or MKL) is also needed for PSE and DPStokes.  

### Usage
MultiMobility exposes three functions:  
  * Mdot(positions, forces)  
    Computes the product of the mobility tensor (M) with the forces acting on each particle position.  
  * stochasticDisplacements(positions)  
    Computes the stochastic displacements, i.e sqrt(2kT M)·dW. Being dW a group of Weinner processes.  
  * hydrodynamicDisplacements(positions, forces)  
    Equivalent to calling Mdot and stochasticDisplacements and summing the results.  

Additionally, MultiMobility requires an initialization, providing the hydrodynamic radius, viscosity and temperature. Optionally, a tolerance can also be specified (for PSE and DPStokes).  

See the examples (example.py or example.cpp) for an usage guide for each language.  
