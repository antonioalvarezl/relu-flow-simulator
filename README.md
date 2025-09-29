# ReLU Neural ODE Density Flow Simulator

Interactive demo to explore density evolution under a piecewise-linear flow driven by a single ReLU unit, with **multi-step composition**, **1D/2D modes**, and **population vs. empirical** views.

**Live:** https://antonioalvarezl.github.io/relu-flow-simulator/  
**Code:** https://github.com/antonioalvarezl/relu-flow-simulator  
**License:** MIT

## Overview

We visualize solutions of the continuity equation
∂_t ρ + ∇·(ρ v) = 0,
with velocity field
v(x) = w (aᵀ x + b)_+,
where (·)_+ = max{0,·}, and w,a ∈ ℝᵈ (with d=1 or d=2).  
A timeline splits the evolution into steps; each step uses its own parameters (w,a,b), and the total map is the composition across steps.

## Quick start

- Online: open the live link above.
- Local: open `index.html` or run:
    python -m http.server 8000
  then visit http://localhost:8000.

## Controls & Options

- Dimension: toggle 1D / 2D.
- Initial condition:
  - Standard Gaussian
  - Uniform [-1,1] in 1D / [-1,1]² in 2D
- Representation:
  - Population (analytical density via closed-form pullbacks)
  - Empirical (particles; choose 10–100 and Resample)
- Multi-step timeline: add/remove steps; per-step sliders for w, a, b.
  - Click on the canvas to set the current step’s b (hyperplane position).
  - Global time slider runs through the whole timeline; Play/Pause and Reset.
- Visualization:
  - Vector field overlay (opacity slider; density slider in 2D).
  - Heatmap resolution (2D).

The info panel shows the current step, time-in-step, λ=⟨w,a⟩, and the Jacobian factor where applicable. In 1D, the total mass estimate is displayed.

## Mathematical background (closed-form map)

Let H⁺={x: aᵀx+b>0} and H⁻={x: aᵀx+b≤0}.  
Within a single step of duration t∈[0,1], the density is updated by a pullback:

- Inactive region H⁻: ρ_t(x)=ρ₀(x) (no change).
- Active region H⁺: define λ=⟨w,a⟩ and A = w aᵀ.

  - Non-degenerate case λ≠0:
    e^(−tA)=I+((e^(−λt)−1)/λ) w aᵀ,
    x₀=e^(−tA)x−(b/λ)(1−e^(−λt)) w,
    ρ_t(x)=ρ₀(x₀) e^(−λt).

  - Degenerate case λ=0:
    e^(−tA)=I−t w aᵀ,
    x₀=(I−t w aᵀ)x − t b w,
    ρ_t(x)=ρ₀(x₀).

For multiple steps, the simulator composes these maps in order.  
In empirical mode, particles follow ẋ = w (aᵀ x + b)_+ with a simple Euler integrator; the population view uses the closed-form pullbacks.

## Usage notes

- 1D view: line plot of the current density, hyperplane location (vertical dashed line), and a row of arrows showing the vector field.
- 2D view: density heatmap, vector field arrows, and the current hyperplane (line).
- Setting b quickly: click or drag on the canvas to update b for the current step.
- Step timing: the global time [0,1] is split evenly across the number of steps.

## Educational applications

- Students: build intuition about ReLU-driven flows; see how hyperplanes gate transport.
- Researchers: sanity-check closed-form behavior and degenerate vs. non-degenerate regimes.
- Educators: use the timeline to stage examples in lectures; switch to particles for a discrete view.

## Credits

If you use this demo in talks or teaching materials, please credit:

> Antonio Alvarez — ReLU Neural ODE Density Flow Simulator (GitHub/Live link)
