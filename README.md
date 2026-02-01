**ALL CODE IN PYTHON**
Results of Running the Code (Excluding Plot Outputs):
Inputs → U_inf = 4 m/s (free-stream velocity), x = 0.3m, B = 0.57 (Only used for part (b)).
PART (a) results (see plots, added checks for B_found and f'(0)≈1 shown:
Blasius curvature (computed via the shooting method), (expct. f''(0) ≈ 0.332 from theory). f''(0) = 0.3320591858096608 after 11
iterations.
Check: f'(zeta_max) (should be ≈1) = 1.0000000000000007
PART (b) results:
y_B (m) = 0.0023405277141144852, y_B (mm) = 2.341 → wall-normal distance where u_x = B·U∞ (x = 300 mm)
u_x (m/s) = 2.2799999999999998 ≈ 2.280 → local streamwise velocity at y_B
u_y (m/s) = 0.0043446423113839 ≈ 0.004 → local wall-normal velocity at y_B
PART (c) results:
δ_99 (m) = 0.0064442677756989825, δ_99 (mm) = 6.444 → boundary-layer thickness where u_x = 0.99*U∞
δ_99_formula (m) = 0.006562678568999094, δ_99_formula (mm) = 6.563 → approximate empirical estimate
(δ_99=5√(νx/U∞)).
% difference = -1.8043% → (δ_99 – δ_99_formula ) / δ_99_formula × 100
δ* (m) = 0.002259, δ* (mm) = 2.259 → displacement thickness (numerical integration up to ζ_max).
CODE APPENDIX:
Grid: zeta_max = 8.0, n_points = 1000
ζ_B_given (b) = 1.783210688674221
ζ_99 (c) = 4.909784707528217
physical dy resolution = 1.051080e-05 m = 10.511μm, this gives many points across the boundary layer.

(Figure Captions from Academic Report given, run code yourself for plot images).

Figure 1 - Part (a) plot of 𝑓′(𝜁) showing the dimensionless velocity profile of (𝑢𝑥/𝑈∞ vs 𝜁) where
𝑓′′(0) = 𝐵found. The appendix provides a plot of a zoomed view corresponding to our given B = 0.57
value. Generated using Python.

Figure 2 - Part (a) plot of our Blasius Stream Function 𝑓(𝜁) vs. Similarity Variable 𝜁.
Generated using Python.
