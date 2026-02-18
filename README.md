# Blasius-Boundary-Layer-Calculator

Python implementation of a numerical **Blasius boundary-layer** solver, using the **shooting method** to recover the canonical Blasius similarity solution and compute physically meaningful boundary-layer quantities.

---

## Overview

This repository contains a full Python solution of the **Blasius boundary-layer problem**, implemented from first principles using numerical methods.

The Blasius ordinary differential equation (ODE) is solved using a shooting method combined with **Brent’s root-finding algorithm**, enforcing the far-field boundary condition that the dimensionless streamwise velocity converges to unity. The solver recovers the classical Blasius curvature value:

```math
f''(0) \approx 0.332
```

The code was developed for an academic fluid mechanics assignment and is written to prioritise clarity, physical interpretation, and numerical validation rather than minimalism.

---

## Governing Equation (Blasius ODE)

The Blasius equation is:

```math
f'''(\zeta) + \tfrac{1}{2} f(\zeta) f''(\zeta) = 0
```

with boundary conditions:

```math
f(0)=0,\quad f'(0)=0,\quad f'(\infty)=1
```

---

## Numerical Method

The third-order Blasius ODE is rewritten as a system of first-order equations and integrated numerically (e.g., using `odeint` or an equivalent integrator).

The unknown wall curvature is treated as the shooting parameter:

```math
B = f''(0)
```

A residual is defined from the far-field mismatch, e.g.:

```math
R(B) = f'(\zeta_{max}; B) - 1
```

Brent’s method is then used to robustly solve the nonlinear root-finding problem:

```math
R(B)=0
```

The computed curvature value (`B_found`) is obtained numerically and is **not imposed**.

A separate spreadsheet value (`B_given = 0.57`) is used only where explicitly required in Part (b) of the assignment and does **not** influence the numerical solution.

---

## Physical Mapping and Parameters

The similarity variable is related to the physical wall-normal coordinate using the standard Blasius scaling (as used in the assignment).

Air at 100 °C is assumed, with kinematic viscosity:

```math
\nu = 2.3\times 10^{-5}\ \mathrm{m^2/s}
```

The solution is evaluated at:
- Streamwise location: `x = 0.3 m`
- Free-stream speed: `U∞ = 4 m/s`

The similarity domain is truncated at:

```math
\zeta_{max}=8
```

which is sufficient for the velocity profile to reach its asymptotic value. A grid of **1000 points** is used, corresponding to a physical wall-normal resolution of approximately **10.5 μm**, enabling accurate interpolation and numerical integration.

---

## Computed Results (Summary)

The shooting method converges to:

```math
f''(0) = 0.332059
```

after 11 residual evaluations.

A consistency check confirms:

```math
f'(\zeta_{max}) \approx 1
```

verifying correct enforcement of the far-field boundary condition.

### Part (b)
The wall-normal location where:

```math
u_x = B_{given}\,U_\infty
```

is identified using interpolation on the computed velocity profile, and the corresponding physical velocities `u_x` and `u_y` are calculated.

### Part (c)
The boundary-layer thickness `delta_99` is computed numerically and compared against the empirical estimate:

```math
\delta_{99} \approx 5\sqrt{\frac{\nu x}{U_\infty}}
```

with a percentage difference of approximately **−1.8%**.

The displacement thickness `delta*` is obtained via numerical integration of the velocity deficit (e.g., trapezoidal rule):

```math
\delta^* = \int_0^{\infty}\left(1-\frac{u}{U_\infty}\right)dy
```

---

## Output and Visualisation

The code generates plots of:
- Dimensionless velocity profile: `f'(ζ)`
- Blasius stream function: `f(ζ)`
- A zoomed appendix plot highlighting the location corresponding to the given spreadsheet value of `B`

All figures are generated programmatically using **Matplotlib** and saved at high resolution for inclusion in reports.

Figure captions used in the original academic submission are included in the repository for reference. Users are expected to run the script locally to regenerate the plots.

---

## Notes on Usage

- `B_found` is computed numerically and represents the physically meaningful Blasius curvature.
- `B_given` is not used in the shooting method and is included only to satisfy the requirements of a specific assignment sub-part.
- Viscosity handling is explicitly documented to avoid ambiguity when converting between similarity and physical coordinates.

---

## Context

This repository is maintained as an academic reference and portfolio artefact.  
It demonstrates numerical ODE solving, root finding, boundary-layer theory, and careful physical interpretation rather than serving as a general-purpose CFD tool.
