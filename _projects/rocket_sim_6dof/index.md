---
layout: post
title: "6DOF Rocket Simulator & Design Studio"
description: >-
  Interactive 6-degrees-of-freedom rocket simulator and design studio built in Python. Features comprehensive physics modeling, real-time rocket design, aerodynamic stability analysis, and 3D visualization for aerospace engineering education and research.
skills:
  - Aerospace Engineering
  - Flight Dynamics
  - Aerodynamics
  - Python
  - PyQt5
  - PyVista
  - SciPy
  - 3D Visualization
  - Physics Simulation
main-image: /preview1.png
lang: en
date: 2025-06-21
---

# 6DOF Rocket Simulator & Design Studio

An interactive 6-degrees-of-freedom (6-DOF) rocket simulator built in Python that provides a comprehensive platform for designing rockets from core components, defining propulsion systems, and launching them in a 3D environment governed by high-fidelity physics models. This simulator serves as a "virtual wind tunnel" and launchpad for understanding the critical relationship between rocket design, aerodynamic stability, and flight paths.

![Rocket Simulator Interface](/_projects/rocket_sim_6dof/roket6dof.gif)

---

## 🚀 Key Features

### Interactive Rocket Design
- **Real-time Design:** Adjust sliders to visually and physically modify rocket dimensions in real-time
- **Geometric Parameters:** Modify body diameter, length, nose cone dimensions, and fin geometry
- **Automatic Calculations:** Dry mass, center of gravity, center of pressure, and rotational inertia automatically recalculated

### Full 6-DOF Physics Engine
- **Complete Motion Simulation:** Both translational (X, Y, Z position) and rotational (pitch, yaw, roll) motion
- **High-Precision Integration:** RK45 (Runge-Kutta-Fehlberg) adaptive step-size solver for accurate results
- **Automatic Termination:** Simulation terminates precisely upon ground impact using solver events

### High-Fidelity Aerodynamics & Stability
- **Dynamic Drag Modeling:** Drag coefficient calculated at every time step based on current Mach number
- **Transonic Effects:** Models critical transonic drag rise phenomenon
- **Stability Analysis:** Realistic aerodynamic restoring torque prevents non-physical behavior
- **Center of Pressure/Gravity:** Dynamic interaction between CP and CG for authentic flight characteristics

### Atmospheric Modeling
- **Standard Atmosphere:** Implements 1976 U.S. Standard Atmosphere model
- **Realistic Properties:** Accurate temperature, pressure, density, and speed of sound vs. altitude
- **Critical for Accuracy:** Essential for precise drag and Mach number calculations

### Interactive 3D Visualization
- **High-Performance Rendering:** Smooth, high-framerate 3D visualization using PyVista
- **Dense Output Integration:** Continuous state interpolation for fluid animation
- **Multiple Camera Modes:**
  - **Chase Camera:** Dynamically follows the rocket
  - **Fit Trajectory:** Shows entire flight path
  - **Free Look:** User-controllable camera with mouse interaction
- **Visual Effects:** Active thrust plume during engine burn and apogee marker

### Customizable Propulsion & Launch
- **Engine Parameters:** Set fuel mass, thrust, and specific impulse (Isp)
- **Burn Time Estimation:** Real-time calculation based on propulsion parameters
- **Thrust Misalignments:** X/Y-axis thrust vectoring to simulate manufacturing imperfections
- **Launch Conditions:** Configurable initial pitch angle from vertical

### Variable Simulation Speed
- **Playback Control:** Real-time, slow-motion, or fast-forward analysis
- **Interactive Analysis:** Pause, rewind, and study specific flight phases

---

## 📐 Physics & Engineering Model

### State Vector (13 Elements)
The complete rocket state captured in vector `y`:
- **Mass (m):** Current total mass in kg
- **Position (x_N):** Inertial position [x, y, z] in meters
- **Velocity (v_N):** Inertial velocity [vx, vy, vz] in m/s
- **Attitude (sigma_BN):** 3-element Modified Rodrigues Parameters (MRP) vector
- **Angular Velocity (omega_BN):** Body-frame angular velocity [wx, wy, wz] in rad/s

### Equations of Motion

#### Translational Dynamics (Newton's Second Law)
```
v̇ = F_net / m
```
**Force Components:**
- **Gravity (F_g):** Constant downward vector [0, 0, -g₀]
- **Thrust (F_thrust):** Engine thrust rotated from body to inertial frame using attitude matrix
- **Drag (F_drag):** Opposes velocity relative to atmosphere using dynamic drag coefficient

#### Rotational Dynamics (Euler's Equations)
```
ω̇ = I⁻¹ × (M_net - ω × (I × ω))
```
**Torque Components:**
- **Thrust Torque (M_thrust):** From misaligned thrust vectors
- **Aerodynamic Torque (M_aero):** Restoring torque for stability (see detailed model below)

### Advanced Physical Models

#### Atmospheric Properties (1976 U.S. Standard Atmosphere)
- **Temperature:** `T = T₀ - L × h` (linear lapse rate in troposphere)
- **Pressure:** `P = P₀ × (1 - L×h/T₀)^(g₀/(R×L))`
- **Density:** `ρ = P/(R×T)`
- **Speed of Sound:** `a = √(γ×R×T)`

#### Mach-Dependent Drag Coefficient
- **Dynamic Calculation:** Linear interpolation over Mach number lookup table
- **Transonic Rise:** Models significant drag increase near Mach 1.0
- **Realistic Behavior:** Typical model rocket aerodynamic characteristics

#### Aerodynamic Stability Model
1. **Angle of Attack (α):** Angle between velocity vector and rocket axis
2. **Normal Force:** `F_normal = q × A_ref × C_Nα × sin(α)` where `q` is dynamic pressure
3. **Center of Pressure:** Geometric estimation from rocket design
4. **Dynamic CG:** Real-time calculation accounting for fuel consumption
5. **Restoring Torque:** `M_aero = (r_cp - r_cg) × F_normal` (stabilizing effect)

#### Attitude Representation (Modified Rodrigues Parameters)
- **Singularity-Free:** Avoids gimbal lock issues of Euler angles
- **Computationally Efficient:** Minimal parameters for 3D rotations
- **Conversion Functions:** MRP ↔ Direction Cosine Matrix transformations

---

## 🖥️ Project Structure

| File | Purpose |
|------|---------|
| `visualizer.py` | Main GUI application, 3D scene setup, user interaction, animation loop |
| `dynamics.py` | Core physics engine, ODE system, atmospheric/aerodynamic models |
| `helpers.py` | Attitude mathematics utilities (MRPs, DCMs, rotations) |
| `main.py` | Legacy basic plotting functionality (superseded by visualizer) |
| `requirements.txt` | Python package dependencies |

**Core Technologies:**
- **PyQt5:** Graphical user interface framework
- **PyVista:** High-performance 3D rendering and visualization
- **SciPy:** Numerical integration and scientific computing
- **NumPy:** Vector mathematics and array operations

---

## 🚀 Quick Start Guide

### Installation
```bash
# Clone repository
git clone https://github.com/daglar510/rocket_sim_6dof.git
cd rocket_sim_6dof

# Create virtual environment
python -m venv .venv

# Activate environment (Windows)
.venv\Scripts\activate
# Activate environment (macOS/Linux)
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Launch simulator
python visualizer.py
```

### User Interface Overview
![Simulator Interface](/_projects/rocket_sim_6dof/preview1.png)

**Left Panel - Design Studio:**
- Rocket geometry sliders with real-time 3D preview
- Propulsion system configuration
- Launch parameters and simulation controls

**Right Panel - 3D Visualization:**
- Interactive 3D rocket model and trajectory
- Multiple camera modes and controls
- Real-time flight parameter display

---

## 📊 Simulation Workflow

1. **Design Phase:** Use sliders to configure rocket geometry and propulsion
2. **Pre-flight Check:** Review estimated mass, CG/CP positions, burn time
3. **Launch Configuration:** Set initial pitch angle and thrust misalignments
4. **Camera Selection:** Choose viewing mode for analysis
5. **Simulation Execution:** Run with variable speed control
6. **Post-flight Analysis:** Study trajectory, stability, and performance

---

## 🎯 Educational Applications

### Learning Objectives
- **Rocket Design Principles:** Understand geometric effects on stability and performance
- **Physics Integration:** Experience 6-DOF motion in realistic environment
- **Aerodynamic Concepts:** Visualize stability derivatives and control authority
- **Propulsion Effects:** Analyze thrust vectoring and misalignment consequences
- **Atmospheric Influences:** Study altitude-dependent aerodynamic phenomena

### Research Applications
- **Design Optimization:** Parametric studies of rocket configurations
- **Stability Analysis:** Monte Carlo analysis of design robustness
- **Control System Development:** Test guidance and control algorithms
- **Educational Tool:** Interactive learning platform for aerospace engineering

---

## 🔧 Technical Specifications

### System Requirements
- **Python Version:** 3.8 or higher
- **Memory:** 8GB RAM minimum (16GB recommended)
- **Graphics:** Dedicated GPU recommended for 3D visualization
- **Operating System:** Windows, macOS, or Linux

### Performance Characteristics
- **Integration Method:** Adaptive Runge-Kutta-Fehlberg (RK45)
- **Time Step Control:** Automatic error-based step size adjustment
- **Dense Output:** Continuous state interpolation for smooth animation
- **Event Detection:** Precise ground impact termination

### Accuracy Features
- **High-Order Integration:** 4th/5th order embedded RK method
- **Adaptive Stepping:** Automatic refinement in critical flight phases
- **Physical Consistency:** Mass conservation and realistic aerodynamic behavior
- **Numerical Stability:** Robust attitude integration using MRPs

---

## 📚 Dependencies

```
numpy>=1.21.0
scipy>=1.7.0
pyvista>=0.35.0
PyQt5>=5.15.0
vtk>=9.1.0
```

---

## 👨‍💻 Development & Support

- **Lead Developer:** Dağlar Duman
- **Institution:** Aerospace Engineering Research
- **License:** MIT License - Open source for educational and research use
- **Repository:** [GitHub](https://github.com/daglar510/rocket_sim_6dof)
- **Contact:** [Email](mailto:daglarduman510@gmail.com) | [LinkedIn](https://www.linkedin.com/in/daglarduman/)

---

## ⚠️ Important Notes

- **Educational Purpose:** Designed for learning and research, not certified flight software
- **Simplified Models:** Some phenomena approximated for computational efficiency
- **Validation Recommended:** Cross-verify results with multiple analysis tools
- **Export Compliance:** Ensure compliance with local regulations for aerospace technology

---

*This 6DOF rocket simulator represents comprehensive aerospace engineering research and development, combining advanced physics modeling with interactive visualization for educational and research purposes. Contributions and collaborations welcome!*