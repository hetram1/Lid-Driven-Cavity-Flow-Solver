# Lid-Driven Cavity Flow Solver (Navier–Stokes)

A 2D Computational Fluid Dynamics (CFD) simulation of incompressible fluid flow inside a square cavity using the Navier–Stokes equations.

The solver is implemented from scratch in Python using:

- Finite Difference Methods
- Explicit time stepping
- Chorin’s Projection Method for pressure–velocity coupling

This project demonstrates the fundamentals of numerical PDE solving, fluid dynamics simulation, and scientific computing.

---

## Preview

Example simulation output:

![Simulation Result](lid_driven_cavity_result.png)

The moving top wall drives the fluid, producing a primary vortex inside the cavity.

- Streamlines → velocity field
- Color map → pressure distribution

---

## Key features

- Implementation of incompressible Navier–Stokes equations
- Finite difference discretization
- Pressure Poisson solver
- Chorin projection method
- Stability-checked explicit time integration
- Velocity streamlines + pressure visualization
- Pure NumPy implementation

---

## Overview

The lid-driven cavity problem is a classical benchmark in computational fluid dynamics.

A square cavity contains fluid. The top wall moves horizontally, dragging the fluid and generating circulation. Over time viscous effects produce a primary vortex inside the cavity.

---

## Governing equations

The simulation solves the incompressible Navier–Stokes equations.

### Momentum equation

```
∂u/∂t + (u · ∇)u = −1/ρ ∇p + ν ∇²u + f
```

### Incompressibility condition

```
∇ · u = 0
```

Where:

| Symbol | Meaning                      |
| -----: | :--------------------------- |
|      u | velocity vector              |
|      p | pressure                     |
|      ν | kinematic viscosity          |
|      ρ | density                      |
|      f | external force               |
|      ∇ | gradient/divergence operator |
|     ∇² | Laplacian                    |

---

## Physical setup

The simulation domain is a unit square cavity.

```
      → → → Moving lid (constant velocity)

1.0 +--------------------------------+
    |                                |
    |                                |
    |                                |
    |                                |
    |                                |
    |                                |
    |                                |
0.0 +--------------------------------+
    0.0                              1.0
```

Boundary conditions:

| Boundary    | Condition                    |
| :---------- | :--------------------------- |
| Top wall    | constant horizontal velocity |
| Bottom wall | u = 0, v = 0                 |
| Left wall   | u = 0, v = 0                 |
| Right wall  | u = 0, v = 0                 |

Initial condition:

```
u = 0
v = 0
p = 0
```

---

## Numerical method

The solver uses Chorin’s projection method (pressure–velocity splitting).

### Step 1 — Tentative velocity

Solve the momentum equation without pressure:

```
∂u/∂t + (u · ∇)u = ν ∇²u
```

### Step 2 — Pressure Poisson equation

```
∇²p = ρ/Δt (∇ · u)
```

This enforces the divergence-free constraint.

### Step 3 — Velocity correction

```
u ← u − Δt/ρ ∇p
```

The corrected velocity field satisfies incompressibility.

---

## Numerical implementation

| Method                 | Purpose                  |
| :--------------------- | :----------------------- |
| Finite difference      | spatial discretization   |
| Central differences    | gradients and divergence |
| Explicit time stepping | time integration         |
| Iterative Poisson      | pressure calculation     |
| Streamline plot        | flow visualization       |

Grid resolution used in this implementation:

```
41 × 41 grid
```

---

## Stability condition

Explicit schemes require a stable timestep:

```
Δt ≤ (0.5 × Δx²) / ν
```

The code checks this condition automatically to prevent unstable simulations.

---

## Project structure

```
lid-driven-cavity/
├── lid_driven_cavity_python_simple.py
├── lid_driven_cavity_result.png
└── README.md
```

---

## Requirements

Python 3.8+

Install dependencies:

```
pip install numpy matplotlib tqdm
```

---

## Running the simulation

Run the solver:

```
python lid_driven_cavity_python_simple.py
```

The script will:

1. simulate fluid motion
2. compute velocity and pressure fields
3. generate streamlines and pressure contours
4. save the visualization

Output file:

```
lid_driven_cavity_result.png
```

---

## What this project demonstrates

Key ideas in scientific computing and CFD:

- numerical solution of partial differential equations
- simulation of Navier–Stokes fluid flow
- finite difference discretization
- pressure–velocity coupling
- visualization of physical simulations

---

## Possible extensions

Potential improvements include:

- higher grid resolution
- Reynolds number experiments
- comparison with Ghia et al. benchmark data
- faster Poisson solvers (Jacobi / Gauss–Seidel / multigrid)
- GPU acceleration

---

## References

- Chorin, A. J. (1968) — _Numerical Solution of the Navier–Stokes Equations_
- Ghia, U., Ghia, K., Shin, C. (1982) — _High-Re solutions for incompressible cavity flow_

---

## Author

Hetram
