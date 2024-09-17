# Molecular-Dynamics
Microcanonical (NVE) molecular dynamics simulation of a Lennard-Jones monoatomic fluid using the velocity Verlet algorithm, inspired by [Frenkel & Smit’s *Understanding Molecular Simulations*](https://www.sciencedirect.com/book/9780122673511/understanding-molecular-simulation).

## Background
Molecular dynamics simulations allow the study a system of atoms or molecules through the use of Newton's equations to predict their trajectories. This allows various thermodynamic properties to be calculated, as well as providing information on the system's structure.

Having read *Frenkel & Smit*, I gave a go at implementing my own molecular dynamics simulation using Python. I chose the microcanonical ensemble (constant number of particles, volume, and energy) and used the Lennard-Jones potential to model the interactions between particles:

$$   U = 4 \epsilon [ (\frac{\sigma}{r})^{12} - (\frac{\sigma}{r})^6 ] $$

where $U$ denotes the potential energy, $\epsilon$ the well depth, $\sigma$ the distance at which the potential is 0, and $r$ the distance between two particles.

Reduced units are used in the code, with the mass of a particle = $\epsilon$ = $\sigma$ = $k_{b}$ = 1. 

## Code
The code can generate .xyz files for visualisation in software such as OVITO, an example of a run being in the folder 'data'. The code can also compute properties such as temperture, pressure, and heat capacity. A radial distribution function is also produced.

Below are the results for a simulation. The initial parameters were:
- Number of time steps = 5000 (Doesn't actually need to be anywhere near this high as the system equilibrates quite quickly, but it does allow the initial equilibration to be averaged out and produces a smoother radial distribution function).
- Number of particles $N$ = 900
- Side of the simulation box $L$ = 10 (Density = 0.9)
- Cutoff distance = 3 $\sigma$
- Time step $dt$ = 0.01
- Initial temperature $T$ = 1 (Note that this will change during the simulation run, but will then remain roughly constant.)

<img src="https://github.com/user-attachments/assets/55c01aec-523b-438f-93b4-2ce8c59a17fd" width="500">
<img src="https://github.com/user-attachments/assets/c455dd71-ce27-41f8-9d44-edad23ff1738" width="500">

Thermodynamic properties:
- Temperature: 1.814 +- 0.002
- Pressure: 1.633 +- 0.002
- Heat capacity = 1.188 x $10^{-6}$

Simulation times will vary depending on the parameters as well as the computer specs. This took about 30 minutues to run.

## Comments and Further Work
I have learnt quite a lot about both Python and molecular dynamics. The code is not optimised, though where possible I have tried (e.g. vectorising instead of using for loops). The code is also not rigorously tested - though the numbers for the energy and force agree with manual calculations for 2 and 3 particle systems.

There are many more things I could explore. Some future goals I would like to do are:
- Implement a thermostat for canonical (NVT) simulations.
- Simulate molecules and/or mixtures.
- Compute other thermodynamic and/or transport properties, e.g. self-diffusion coefficient.
- Calculate statistical errors using block averaging.
- General optimisation.
