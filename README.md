# Simple Neural ODE Density Flow Simulator

Interactive demo to explore density evolution under a piecewise-linear flow driven by a single ReLU unit, with **multi-step composition**, **dimension 1 or 2**, and **population vs. empirical** views.

**Live:** https://antonioalvarezl.github.io/relu-flow-simulator/  
**Code:** https://github.com/antonioalvarezl/relu-flow-simulator  
**License:** MIT

## Overview

We visualize solutions of the continuity equation:

$$
\\partial_t \\rho(x,t) + \\nabla \\cdot (\\rho(x,t)\\, v(x)) = 0
$$

with velocity field

$$
v(x) = w \\, \\max(0, a^\\top x + b),
$$

for $w,a \\in \\mathbb{R}^d$ ($d = 1$ or $d=2$).

A timeline splits the evolution into steps; each step uses its own parameters $(w,a,b)$, and the total map is the composition across steps.

## Quick start

- **Online:** open the live link above.
- **Local:** open `index.html` directly in your browser.

## Controls & Options

- **Dimension:** toggle 1D / 2D.
- **Initial condition:**
  - Standard Gaussian
  - Uniform $[-1,1]$ in 1D / $[-1,1]^2$ in 2D
- **Representation:**
  - **Population** (analytical density via closed-form pullbacks)
  - **Empirical** (particles; choose 10–100 and Resample)
- **Multi-step timeline:** add/remove steps; per-step sliders for $w$, $a$, $b$.  
  - Click on the **canvas** to set the current step’s $b$ (hyperplane position).  
  - **Global time** slider runs through the whole timeline; **Play/Pause** and **Reset**.
- **Visualization:**  
  - **Vector field** overlay (opacity slider; density slider in 2D).  
  - **Heatmap resolution** (2D).

The info panel shows the current step, time-in-step, the value of $w \\cdot a$, and the Jacobian factor where applicable. In 1D, the total mass estimate is displayed.

## Mathematical background (closed-form map)

Let $H^+ = \\{x : a^\\top x + b > 0\\}$ and $H^- = \\{x : a^\\top x + b \\leq 0\\}$.

- **Inactive region $H^-$:**

$$
\\rho_t(x) = \\rho_0(x)
$$

- **Active region $H^+$:**

  If $w \\cdot a \\neq 0$:

$$
e^{-t w a^\\top} = I + \\frac{e^{-t (w \\cdot a)} - 1}{w \\cdot a} \\, w a^\\top
$$

$$
x_0 = e^{-t w a^\\top} x - \\frac{b}{w \\cdot a}\\big(1 - e^{-t (w \\cdot a)}\\big) w
$$

$$
\\rho_t(x) = \\rho_0(x_0) \\, e^{-t (w \\cdot a)}
$$

  If $w \\cdot a = 0$:

$$
e^{-t w a^\\top} = I - t w a^\\top
$$

$$
x_0 = (I - t w a^\\top) x - t b w
$$

$$
\\rho_t(x) = \\rho_0(x_0)
$$

For multiple steps, the simulator composes these maps in order.  

In **empirical** mode, particles follow

$$
\\dot x = w \\, \\max(0, a^\\top x + b).
$$

## Usage notes

- **1D view:** line plot of the current density, hyperplane location (vertical dashed line), and a row of arrows showing the vector field.
- **2D view:** density heatmap, vector field arrows, and the current hyperplane (line).
- **Setting $b$ quickly:** click or drag on the canvas to update $b$ for the current step.
- **Step timing:** the global time $[0,1]$ is split evenly across the number of steps.

## Educational applications

- **Students:** build intuition about ReLU-driven flows; see how hyperplanes gate transport.
- **Researchers:** sanity-check closed-form behavior and degenerate vs. non-degenerate regimes.
- **Educators:** use the timeline to stage examples in lectures; switch to particles for a discrete view.

## Credits

If you use this demo in **talks or teaching materials**, please credit:

> Antonio Alvarez — *ReLU Neural ODE Density Flow Simulator* (GitHub/Live link)
