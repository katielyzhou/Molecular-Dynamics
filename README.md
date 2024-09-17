# Molecular-Dynamics
Microcanonical (NVE) molecular dynamics simulation of a Lennard-Jones monoatomic fluid using the velocity Verlet algorithm, inspired by [Frenkel & Smit’s **Understanding Molecular Simulations*](https://www.sciencedirect.com/book/9780122673511/understanding-molecular-simulation).

## Background
Molecular dynamics simulations allow the study a system of atoms or molecules through the use of Newton's equations to predict their trajectories. This allows various thermodynamic properties to be calculated, as well as providing information on the system's structure.

Having read *Frenkel & Smit*, I gave a go at implementing my own molecular dynamics simulation using Python. I chose the microcanonical ensemble (constant number of particles, volume, and energy) and used the Lennard-Jones potential to model the interactions between particles:

$$   U = 4 \epsilon [ (\frac{\sigma}{r})^{12} - (\frac{\sigma}{r})^6 ] $$

where $U$ denotes the potential energy, $\epsilon$ the well depth, $\sigma$ the distance at which the potential is 0, and $r$ the distance between two particles.

## Code
The code can generate .xyz files for visualisation in software such as OVITO, as well compute properties such as temperture, pressure, heat capacity, and the self-diffusion coefficient. A radial distribution function is also produced.

## Comments and Further Work
I have learnt quite a lot about both Python and molecular dynamics. The code is not optimised, though where possible I have tried (e.g. vectorising instead of using for loops). The code is also not rigorously tested - though the numbers for the energy and force agree with manual calculations for 2 and 3 particle systems.

There are many more things I could explore. Some future goals I would like to do are:
- Implement a thermostat for canonical (NVT) simulations.
- Simulate molecules and/or mixtures.
- Compute other thermodynamic or transport properties, e.g. velocity autocorrelation function .
- Calculate statistical errors using block averaging.
