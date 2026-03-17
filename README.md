# Lid-Driven Cavity Flow Solver (Navier–Stokes)

A numerical simulation of **incompressible fluid flow** inside a square cavity using the **Navier–Stokes equations**.

The solver is implemented from scratch using **Finite Difference Methods**, **explicit time stepping**, and **Chorin's Projection Method** to enforce incompressibility.

This project demonstrates core concepts in **computational fluid dynamics (CFD)** and **scientific computing**.

---

## Overview

The **lid-driven cavity** is a classical benchmark problem in CFD.

A square cavity contains fluid.  
The **top wall moves horizontally**, dragging the fluid and generating a circulating flow inside the cavity.

Over time, viscous effects cause the fluid to form a **primary vortex** in the center.

This benchmark is widely used to validate numerical solvers for the **incompressible Navier–Stokes equations**.

---

## Governing Equations

The simulation solves the **incompressible Navier–Stokes equations**:

### Momentum Equation

∂u/∂t + (u · ∇)u = −1/ρ ∇p + ν ∇²u + f

### Incompressibility Constraint

∇ · u = 0

Where:

| Symbol | Meaning                      |
| ------ | ---------------------------- |
| **u**  | velocity vector              |
| **p**  | pressure                     |
| **ν**  | kinematic viscosity          |
| **ρ**  | density                      |
| **f**  | external forcing (set to 0)  |
| **∇**  | gradient/divergence operator |
| **∇²** | Laplacian operator           |

---

## Physical Scenario

The simulation domain is a **unit square cavity**.

            → → → moving lid (u = constant)

1.0 +----------------------------------------+
| |
| |
| |
| |
| |
| |
| |
| |
0.0 +----------------------------------------+
0.0 1.0

Boundary conditions:

| Boundary    | Condition                    |
| ----------- | ---------------------------- |
| Top wall    | constant horizontal velocity |
| Bottom wall | u = 0, v = 0                 |
| Left wall   | u = 0, v = 0                 |
| Right wall  | u = 0, v = 0                 |

Initial condition:

u = 0
v = 0
p = 0

---

## Numerical Method

The solver uses **Chorin's Projection Method**, which splits the Navier–Stokes equations into simpler steps.

### Step 1 — Tentative Velocity

Solve the momentum equation **without pressure**:

∂u/∂t + (u · ∇)u = ν ∇²u

---

### Step 2 — Pressure Poisson Equation

Compute pressure by solving:

∇²p = ρ/Δt (∇ · u)

This ensures the velocity field becomes **divergence-free**.

---

### Step 3 — Velocity Correction

Correct the velocity using the pressure gradient:

u ← u − Δt/ρ ∇p

This enforces **incompressibility**.

---

## Numerical Implementation

The solver uses:

| Method                   | Description               |
| ------------------------ | ------------------------- |
| Finite Difference        | spatial discretization    |
| Central Differences      | gradients and divergence  |
| Explicit Time Stepping   | temporal integration      |
| Iterative Poisson Solver | pressure equation         |
| Streamline Visualization | flow field representation |

Grid resolution:

41 × 41 grid

---

## Stability Condition

Explicit schemes require a stable timestep:

Δt ≤ (0.5 \* Δx²) / ν

The code automatically checks this condition to prevent unstable simulations.

---

## Example Result

The solver produces a **primary vortex inside the cavity**.

- fluid moves right along the lid
- circulates clockwise
- forms a stable vortex

Example output:

![Simulation Result](lid_driven_cavity_result.png)

Blue and red colors represent **pressure distribution**, while streamlines show **velocity flow paths**.

---

## Project Structure

lid-driven-cavity/
│
├── lid_driven_cavity_python_simple.py
├── lid_driven_cavity_result.png
├── README.md

---

## Requirements

Python 3.8+

Install dependencies:

pip install numpy matplotlib tqdm

---

## Running the Simulation

python lid_driven_cavity_python_simple.py

The script will:

1. run the CFD simulation
2. compute velocity and pressure fields
3. generate the visualization
4. save the result as:

lid_driven_cavity_result.png

---

## What This Project Demonstrates

This project showcases understanding of:

- numerical solution of **partial differential equations**
- **Navier–Stokes fluid dynamics**
- **finite difference discretization**
- **pressure–velocity coupling**
- **scientific visualization**

It serves as a compact example of a **CFD solver implemented from scratch**.

---

## Possible Improvements

Future enhancements could include:

- higher grid resolution
- Reynolds number studies
- comparison with **Ghia et al. benchmark data**
- faster pressure solvers (Jacobi / Gauss–Seidel / multigrid)
- GPU acceleration

---

## References

- Chorin, A. J. (1968). _Numerical solution of the Navier–Stokes equations._
- Ghia, U., Ghia, K. N., & Shin, C. T. (1982). _High-Re solutions for incompressible flow using the Navier–Stokes equations._

---

## Author

Hetram Gugrwal  
B.Tech Chemical Engineering  
IIT Patna
