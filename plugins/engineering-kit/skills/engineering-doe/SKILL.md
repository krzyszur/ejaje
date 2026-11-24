---
name: engineering-doe
description: Plan and optimize simulation or experiment campaigns for engineering problems: screening, space-filling, surrogate models, adaptive sampling, trend fits with uncertainty.
---

# Engineering DoE workflow

Use when a question needs many simulations/measurements to find dependencies or an optimum. Goal: max insight per compute, never fill the full grid blindly.

## 0. Frame
- List inputs (ranges, units, fixed vs free), outputs, constraints (e.g. stiffness >= X), and the desired region. Write them in PROJECT.md.
- Define stopping criteria up front (CI width, R²/Q², decision no longer changes).

## 1. Screening (cheap)
- Morris elementary effects (SALib) or fractional factorial / Plackett–Burman, ~10–20 runs per parameter.
- Rank effects; freeze parameters with negligible effect. Use dimensionless groups (ratios like Ø/pitch, t/Ø) to cut dimensions.

## 2. Space-filling base design
- Latin Hypercube or Sobol (scipy.stats.qmc), ~10×d points in the reduced space, focused on the region of interest.
- Add 3–6 replicates at a few points for type A (noise) uncertainty.

## 3. Surrogate + fit
- Fit RSM (statsmodels OLS, 2nd order) and/or Gaussian process (scikit-learn). Report coefficients with CI, p-values, R², Q² (cross-validation), residual plots. Expanded uncertainty k=2.
- Global sensitivity (Sobol indices) on the surrogate.

## 4. Adaptive sampling
- Next batch of 20–50 points where GP std is largest, near constraint boundaries, or by Expected Improvement (scikit-optimize/BoTorch) when optimizing.
- Re-fit, repeat until stopping criteria met.

## 5. Report
- Charts with shaded desired region, fit line + confidence band, data points; state model and its validity range; never extrapolate trends beyond data.
- Key numbers table: optimum, sensitivities (+10% param -> ±x% output), feasible window.

## Practicalities
- Python tools in venv + requirements.txt (SALib, scipy, scikit-learn, statsmodels, pyDOE3, scikit-optimize).
- Heavy compute runs locally on the user's machine via scripts/queues that skip finished cases; the agent prepares scripts, does not burn tokens on compute.
- Keep large outputs (renders) out of git.
