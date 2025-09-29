# ReLU Neural ODE Density Flow Simulator - Documentation

## Overview
This documentation provides detailed information about the mathematical foundations and implementation of the ReLU Neural ODE Density Flow Simulator.

## Mathematical Foundations

### 1. Neural ODE Formulation
The system is described by the ordinary differential equation:
```
dx/dt = f(x) = max(0, wx + b)
```

Where:
- `x(t)` is the state variable
- `w` is the weight parameter
- `b` is the bias parameter
- `max(0, ·)` is the ReLU activation function

### 2. Density Evolution Equation
The evolution of probability density ρ(x,t) follows the continuity equation:
```
∂ρ/∂t + ∂/∂x[f(x)ρ] = 0
```

### 3. Closed-Form Solutions

#### Case 1: Positive Weight (w > 0)
For the active region where `wx + b > 0`:
```
x(t) = (x₀ + b/w)e^(wt) - b/w
```

The density transforms as:
```
ρ(x,t) = ρ₀((x + b/w)e^(-wt) - b/w) · e^(-wt)
```

#### Case 2: Negative Weight (w < 0)
For `wx + b > 0`:
```
x(t) = (x₀ + b/w)e^(wt) - b/w
```

The density evolution becomes:
```
ρ(x,t) = ρ₀((x + b/w)e^(-wt) - b/w) · |e^(-wt)|
```

#### Case 3: Zero Weight (w = 0)
Simple translation:
```
x(t) = x₀ + bt
ρ(x,t) = ρ₀(x - bt)
```

### 4. Boundary Conditions
When particles reach the inactive region (`wx + b ≤ 0`), they stop evolving and may accumulate at the boundary `x = -b/w`.

## Implementation Details

### Numerical Aspects
- Grid resolution: 200 points
- Domain: x ∈ [-4, 4], ρ ∈ [0, 3]
- Analytical solutions (no numerical integration required)

### Visualization
- Real-time parameter adjustment
- Smooth animation capabilities
- Interactive controls with immediate feedback

### Supported Initial Distributions
1. **Gaussian**: σ-parameterized normal distribution
2. **Uniform**: Constant density over [-1, 1]
3. **Bimodal**: Mixture of two Gaussians

## Usage Examples

### Example 1: Exponential Growth (w > 0, b = 0)
- Set w = 1.0, b = 0.0
- Choose Gaussian initial distribution
- Observe density spreading and tailing

### Example 2: Boundary Accumulation (w > 0, b < 0)
- Set w = 1.0, b = -0.5
- Watch particles accumulate at x = 0.5

### Example 3: Pure Translation (w = 0)
- Set w = 0.0, b = 1.0
- Observe density shifting without deformation

## Technical Specifications

### Browser Requirements
- HTML5 Canvas support
- ES6+ JavaScript compatibility
- CSS Grid and Flexbox support

### Performance
- Optimized for real-time interaction
- Efficient analytical computations
- Responsive design for various screen sizes

## Future Extensions
- Multi-neuron systems
- Alternative activation functions
- 3D density visualizations
- Parameter sensitivity analysis