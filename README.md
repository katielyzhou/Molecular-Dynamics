# Molecular-Dynamics
Microcanonical (NVE) molecular dynamics simulation of a Lennard-Jones monoatomic fluid using the velocity Verlet algorithm, inspired by [Frenkel & Smit’s *Understanding Molecular Simulations*](https://www.sciencedirect.com/book/9780122673511/understanding-molecular-simulation).

## Background
Molecular dynamics simulations allow the study a system of atoms or molecules through the use of Newton's equations to predict their trajectories. This allows various thermodynamic properties to be calculated, as well as providing information on the system's structure.

Having read *Frenkel & Smit*, I gave a go at implementing my own molecular dynamics simulation using Python. I chose the microcanonical ensemble (constant number of particles, volume, and energy) and used the truncated and shifted Lennard-Jones potential to model the interactions between particles:

$$ U = \begin{cases}
        U_{LJ}(r) - U_{LJ}(r_{c}) & r \leq r_{c} \\
        0 & r > r_{c}
        \end{cases} $$

where

$$  U_{LJ}(r) = 4 \epsilon [ (\frac{\sigma}{r})^{12} - (\frac{\sigma}{r})^6 ] $$

$U_{LJ}$ denotes the Lennard-Jones potential, $\epsilon$ the well depth, $\sigma$ the distance at which the potential is 0, and $r$ the distance between two particles with $r_{c}$ the cutoff distance for interactions.

Reduced units are used in the code, with the mass of a particle = $\epsilon$ = $\sigma$ = $k_{b}$ = 1. SI units could be used with care taken for conversions.

## Code
The code can generate .xyz files for visualisation in software such as OVITO, an example of a run being in the folder 'data'. The code can also compute properties such as temperture and pressure. A radial distribution function is also produced.

### Example
Below are the results for a simulation. I used similar conditions as a case study in F&S. The parameters were:
- Number of time steps = 2500 (Doesn't actually need to be near this high as the system equilibrates quite quickly, but it does allow the initial equilibration to be averaged out and produces a smoother radial distribution function).
- Number of particles $N$ = 108
- Side of the simulation box $L$ = 5.038789 (Density = 0.8442)
- Cutoff distance = 2.5 $\sigma$
- Time step $dt$ = 0.01
- Initial temperature $T$ = 0.728 (This will change during the simulation run, but should remain roughly constant.)

<img src="https://github.com/user-attachments/assets/be365dba-b95e-4556-af90-01c9e01dfb5b" width="500">
<img src="https://github.com/user-attachments/assets/585cf6fb-9cde-4010-b779-0382af99993f" width="500">

Simulation times will vary depending on the parameters as well as the computer specs. This took about a minute to run, or 30 seconds if I chose not to save the position data.

Thermodynamic properties:
- Temperature: 1.56234 +/- 0.00885
- Pressure: 5.61335 +/- 0.05588
- Kinetic energy per particle: 2.34351 +/- 0.01327
- Potential energy per particle: -4.33205 +/- 0.01336

Compared to the F&S case study (108 particles, T = 0.728, density = 0.8442):
- Temperature: 1.5043 +/- 0.0008
- Pressure: 5.16 +/- 0.02
- Kinetic energy per particle: 2.2564 +/- 0.0012
- Potential energy per particle: -4.4190 +/- 0.0012

The errors calculated from mine are the standard errors, whilst F&S are from block averages. Differences in the values are due the differences in the initial conditions (position and velocity).

### Visualisation with OVITO:

Files were generated every 20 steps, and the animation is 25 frames a second. The particles' size have been scaled down to 50%.

![simulation](https://github.com/user-attachments/assets/95f2bb4b-5a1b-4be7-8000-364ab31f43d8)

## Comments and Further Work
I have learnt quite a lot about both Python and molecular dynamics. Some caveats though are that the code is not optimised, though where possible I have tried (e.g. vectorising instead of using for loops), and that the code is not rigorously tested.

There are many more things I could explore. Some future things I would like to do are:
- Implement a thermostat for canonical (NVT) simulations.
- Simulate molecules and/or mixtures.
- Compute other thermodynamic and/or transport properties, e.g. self-diffusion coefficient.
- Calculate statistical errors using block averaging.
- General optimisation.
