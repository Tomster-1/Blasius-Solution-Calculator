# Blasius-Boundary-Layer-Calculator

Python implementation of a numerical Blasius boundary-layer solver, using the shooting method to recover the canonical Blasius similarity solution and compute physically meaningful boundary-layer quantities.

---

## Overview

This repository contains a full Python solution of the Blasius boundary-layer problem, implemented from first principles using numerical methods.

The Blasius ordinary differential equation is solved using a shooting method combined with Brent’s root-finding algorithm, enforcing the far-field boundary condition that the dimensionless streamwise velocity converges to unity. The solver recovers the classical Blasius curvature value fpp0 ≈ 0.332, consistent with theory.

The code was developed for an academic fluid mechanics assignment and is written to prioritise clarity, physical interpretation, and numerical validation rather than minimalism.

---

## Numerical Method

The third-order Blasius ODE is rewritten as a system of first-order equations and integrated using `odeint`.

The unknown wall curvature fpp0 is treated as a shooting parameter. A residual is defined as the mismatch between the computed far-field velocity gradient and its theoretical asymptotic value. Brent’s method is then used to solve this nonlinear root-finding problem robustly.

The computed curvature value (`B_found`) is obtained numerically and is not imposed. A separate spreadsheet value (`B_given = 0.57`) is used only where explicitly required in Part (b) of the assignment and does not influence the numerical solution.

---

## Physical Mapping and Parameters

The similarity variable zeta is related to the physical wall-normal coordinate using the standard Blasius scaling.

Air at 100 °C is assumed, with a kinematic viscosity of  
nu = 2.3e-5 m^2/s, assuming atmospheric pressure.

The solution is evaluated at a streamwise location of x = 0.3 m with a free-stream velocity of U_inf = 4 m/s.

The similarity domain is truncated at zeta_max = 8, which is sufficient for the velocity profile to reach its asymptotic value. A grid of 1000 points is used, corresponding to a physical wall-normal resolution of approximately 10.5 microns, ensuring accurate interpolation and numerical integration.

---

## Computed Results (Summary)

The shooting method converges to a curvature value of  
fpp0 = 0.332059, after 11 residual evaluations.

A consistency check confirms that  
fp(zeta_max) ≈ 1, verifying correct enforcement of the far-field boundary condition.

For Part (b), the wall-normal location where  
u_x = B_given × U_inf  
is identified using interpolation on the computed velocity profile, and the corresponding physical velocities u_x and u_y are calculated.

For Part (c), the boundary-layer thickness delta_99 is computed numerically and compared against the empirical estimate  
delta_99 ≈ 5 × sqrt(nu × x / U_inf),  
with a percentage difference of approximately −1.8%.

The displacement thickness delta_star is obtained via numerical integration of the velocity deficit using the trapezoidal rule.

---

## Output and Visualisation

The code generates plots of the dimensionless velocity profile fp(zeta), the Blasius stream function f(zeta), and a zoomed appendix plot highlighting the location corresponding to the given spreadsheet value of B.

All figures are generated programmatically using Matplotlib and saved at high resolution for inclusion in reports.

Figure captions used in the original academic submission are included in the repository for reference. Users are expected to run the script locally to regenerate the plots.

---

## Notes on Usage

`B_found` is computed numerically and represents the physically meaningful Blasius curvature.

`B_given` is not used in the shooting method and is included only to satisfy the requirements of a specific assignment sub-part.

Viscosity handling is explicitly documented to avoid ambiguity when converting between similarity and physical coordinates.

---

## Context

This repository is maintained as an academic reference and portfolio artefact.  
It demonstrates numerical ODE solving, root finding, boundary-layer theory, and careful physical interpretation rather than serving as a general-purpose CFD tool.
