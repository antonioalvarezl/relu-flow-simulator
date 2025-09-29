# ReLU Neural ODE Density Flow Simulator

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.placeholder.svg)](https://doi.org/10.5281/zenodo.placeholder)

An interactive web-based simulator for visualizing probability density evolution under the flow of single-neuron ReLU neural ODEs. This tool provides real-time visualization of closed-form solutions for educational and research purposes.

## 🎯 Overview

This simulator demonstrates the evolution of probability densities under the dynamics of a simple neural ODE with ReLU activation:

```
ẋ = max(0, wx + b)
```

Where `w` is the weight, `b` is the bias, and `x` represents the state variable. The simulator provides an interactive interface to explore how different parameters affect the density evolution over time.

## 🚀 Quick Start

### Online Version
Visit the [live simulator](https://antonioalvarezl.github.io/relu-flow-simulator/) to use the tool directly in your browser.

### Local Installation
1. Clone this repository:
   ```bash
   git clone https://github.com/antonioalvarezl/relu-flow-simulator.git
   cd relu-flow-simulator
   ```

2. Open `index.html` in your web browser or serve it locally:
   ```bash
   python -m http.server 8000  # Python 3
   # or
   python -m SimpleHTTPServer 8000  # Python 2
   ```

3. Navigate to `http://localhost:8000` in your browser.

## 📊 Features

- **Interactive Parameter Control**: Adjust weight (`w`), bias (`b`), and time (`t`) using intuitive sliders
- **Multiple Initial Distributions**: Choose from Gaussian, uniform, or bimodal initial densities
- **Real-time Visualization**: See density evolution updated instantly as you modify parameters
- **Animation Mode**: Watch the temporal evolution of densities with smooth animation
- **Data Export**: Export simulation data as CSV for further analysis
- **Responsive Design**: Works on desktop, tablet, and mobile devices
- **Mathematical Background**: Integrated explanation of the underlying theory

## 🧮 Mathematical Background

### Neural ODE System
The system is governed by the differential equation:
```
ẋ = max(0, wx + b)
```

### Closed-Form Solution
For the density evolution, we have different cases depending on the weight parameter:

**Case 1: w > 0 (Exponential Growth in Active Region)**
- Active region (wx + b > 0): `ρ(x,t) = ρ₀((x - bt)e^(-wt)) · e^(-wt)`
- Inactive region (wx + b ≤ 0): Particles accumulate at the boundary `x = -b/w`

**Case 2: w < 0 (Exponential Decay)**
- Active region: `ρ(x,t) = ρ₀((x - bt)e^(|w|t)) · e^(|w|t)`
- Inactive region: `ρ(x,t) = ρ₀(x)` (no evolution)

**Case 3: w = 0 (Linear Translation)**
- All points: `ρ(x,t) = ρ₀(x - bt)`

### Initial Distributions
The simulator supports three initial distribution types:

1. **Gaussian**: `ρ₀(x) = (1/(σ√(2π))) exp(-x²/(2σ²))`
2. **Uniform**: `ρ₀(x) = 0.5` for `x ∈ [-1,1]`, `0` otherwise
3. **Bimodal**: Mixture of two Gaussians centered at `x = ±1`

## 🎮 Usage Guide

### Basic Controls
1. **Weight (w)**: Controls the strength and direction of the flow
   - Positive values: Exponential growth in active region
   - Negative values: Exponential decay
   - Zero: Pure translation

2. **Bias (b)**: Shifts the activation threshold
   - Determines where ReLU switches from inactive to active

3. **Time (t)**: Evolution time parameter
   - Use slider for precise control
   - Use "Animate Flow" for temporal visualization

4. **Initial Distribution**: Choose the starting probability density
   - Gaussian: Standard normal-like distribution
   - Uniform: Constant density over interval
   - Bimodal: Two-peaked distribution

### Advanced Features
- **Animation**: Click "Animate Flow" to see temporal evolution
- **Reset**: Return to initial state (t = 0)
- **Export Data**: Download CSV file with density values for analysis

### Interpretation Tips
- **Blue curve**: Initial density ρ₀(x)
- **Red curve**: Evolved density ρ(x,t)
- Watch how the red curve changes as you adjust parameters
- Notice accumulation effects when particles hit inactive regions

## 📚 Educational Applications

This simulator is designed for:

### Students
- Visualize abstract concepts in neural ODEs
- Understand ReLU activation effects on dynamics
- Explore different parameter regimes interactively

### Researchers
- Validate theoretical predictions
- Generate publication-quality visualizations
- Test hypotheses about density evolution

### Educators
- Demonstrate neural ODE concepts in lectures
- Create interactive assignments and exercises
- Provide hands-on exploration tools

## 🔬 Technical Implementation

### Architecture
- **Frontend**: Pure HTML5, CSS3, and JavaScript (ES6+)
- **Visualization**: HTML5 Canvas API for high-performance rendering
- **Mathematics**: Closed-form analytical solutions (no numerical integration)
- **Responsive**: CSS Grid and Flexbox for adaptive layouts

### Browser Compatibility
- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+

### Performance
- Real-time rendering at 60 FPS
- Efficient analytical computations
- Optimized canvas drawing operations

## 📖 Citation

If you use this simulator in your research or educational materials, please cite:

### BibTeX
```bibtex
@misc{alvarez2024relu,
  title={ReLU Neural ODE Density Flow Simulator: An Interactive Tool for Visualizing Probability Density Evolution},
  author={Alvarez, Antonio},
  year={2024},
  url={https://github.com/antonioalvarezl/relu-flow-simulator},
  note={Interactive web-based simulator for educational and research purposes},
  doi={10.5281/zenodo.placeholder}
}
```

### APA Style
Alvarez, A. (2024). *ReLU Neural ODE Density Flow Simulator: An Interactive Tool for Visualizing Probability Density Evolution*. GitHub. https://github.com/antonioalvarezl/relu-flow-simulator

### IEEE Style
A. Alvarez, "ReLU Neural ODE Density Flow Simulator: An Interactive Tool for Visualizing Probability Density Evolution," GitHub, 2024. [Online]. Available: https://github.com/antonioalvarezl/relu-flow-simulator

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues, feature requests, or pull requests.

### Development Setup
1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes and test thoroughly
4. Submit a pull request with detailed description

### Areas for Contribution
- Additional initial distributions
- Enhanced visualization options
- Mobile optimization improvements
- Mathematical extensions (multi-neuron systems)
- Performance optimizations

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Inspired by research in neural differential equations
- Built with modern web technologies for accessibility
- Designed for the mathematical and machine learning communities

## 📞 Contact

- **Author**: Antonio Alvarez
- **Repository**: [https://github.com/antonioalvarezl/relu-flow-simulator](https://github.com/antonioalvarezl/relu-flow-simulator)
- **Issues**: [GitHub Issues](https://github.com/antonioalvarezl/relu-flow-simulator/issues)

---

*This tool is designed to make neural ODE concepts accessible and interactive for learners and researchers worldwide.*
