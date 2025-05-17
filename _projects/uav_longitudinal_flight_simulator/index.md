---
layout: post
title: "UAV Longitudinal Flight Dynamics Simulator"
description: >-
  A technical report for our open-source UAV longitudinal flight dynamics simulator project.
  This report covers UAV modeling, input control, state-space simulation, visualization systems,
  aerodynamic and stability analyses, sensor integration, safety features, and system requirements.
skills:
  - Aerospace Engineering
  - Flight Dynamics
  - Python
  - Control Systems
  - Data Visualization
main-image: /figure_1.png
lang: en
---

## Project Overview

The **UAV Longitudinal Flight Dynamics Simulator** is an open-source Python tool developed to simulate and visualize the longitudinal (pitch-axis) flight behavior of UAVs. This report documents the development and testing of the simulation system, covering UAV modeling, aerodynamic and control analysis, and real-time visualizations. It also outlines the integration of elevator input profiles and system stability assessment tools.

---

## 1. UAV Modeling, Simulation & Visualization

### 1.1 UAV Specifications

- **Supported Models:**  
  - Baykar TB2  
  - TUSAŞ Anka  
  - Aksungur  
  - Vestel Karayel  
  - General Atomics Predator  
  - IAI Heron  
- **Flight Axis Simulated:**  
  - Longitudinal (Pitch Axis)

### 1.2 Simulation Overview

The tool enables users to simulate the pitch-axis response of UAVs to various elevator input types. Key aspects include:

- **State-Space Modeling:**  
  UAVs are modeled using linearized state-space representations.  
- **Numerical Integration:**  
  The system uses Runge-Kutta methods (`scipy.solve_ivp`) to simulate time-domain responses.
- **Visualization:**  
  2D plots and 3D phase-space visualizations show state evolution.

*Example Diagram:*  
{% include image-gallery.html images="figure_1_3D.png" height="300" %}

---

## 2. Input Control & Flight Data

The simulator supports different elevator input types and computes the corresponding flight responses:

- **Step Input:**  
  Simulates a sudden elevator deflection.
- **Doublet Input:**  
  Used to analyze damping and short-period response.
- **Custom Input:**  
  User-defined elevator time-series input.

Each input profile affects pitch rate, angle of attack, forward velocity deviation, and pitch angle, which are visualized in simulation outputs.

---

## 3. Sensor Integration & Control Feedback

Although the simulation operates in software, sensor models and control feedback are considered:

- **Virtual IMU Simulation:**  
  Simulates output from a 10 DOF IMU (acceleration, gyro, orientation).
- **Virtual Sensor Models:**  
  Mimics behavior of realistic flight sensors to allow for control loop testing.
- **Control Feedback (Planned):**  
  PID/State-feedback control modules are under development for closed-loop response testing.

---

## 4. Aerodynamics & Stability Analysis

Aerodynamic and stability parameters are derived from each UAV’s geometry and coefficients:

- **Aerodynamic Database:**  
  Pre-loaded aerodynamic models for each UAV.
- **Mode Identification:**  
  The system detects and characterizes phugoid and short-period modes.
- **Stability Metrics:**  
  Calculates eigenvalues, natural frequency, and damping ratio in real-time.

---

## 5. Propulsion & System Characteristics

### 5.1 Propulsion Approximation

While propulsion is not actively modeled in longitudinal analysis, a constant-speed assumption is used:
- **Speed Preset:**  
  Simulated UAVs fly at trimmed cruise conditions (~100–200 km/h depending on model).
- **Disturbance Response:**  
  Inputs affect longitudinal axis only; propulsion modeled as steady-state.

### 5.2 System Constraints

- **Numerical Stability:**  
  Integration step size and stiffness are managed by `solve_ivp`.
- **Data Scaling:**  
  Inputs and outputs are normalized for visualization.

---

## 6. Visual Output & Result Interpretation

### 6.1 2D Time-Domain Plots

Plots include:
- Forward speed deviation (u)
- Angle of attack (α)
- Pitch rate (q)
- Pitch angle (θ)
- Elevator input

### 6.2 3D Phase-Space Visualization

A 3D plot shows evolution in the α–q–θ state-space, highlighting stability characteristics and control response.

---

## 7. Safety Checks & Simulation Limits

To ensure accurate and safe simulations, the following checks are implemented:

- **Numerical Instability Detection:**  
  Alerts users if simulation diverges.
- **State Clipping:**  
  Prevents unrealistic values from visualizing.
- **Input Validation:**  
  Elevator inputs are checked for format and range.

---

## 8. System Architecture & Communication

The simulation tool is modular and extendable:

- **Language:**  
  Python 3.x
- **Libraries Used:**  
  NumPy, SciPy, Matplotlib
- **Architecture:**  
  Input parser → State-space solver → Visualizer

---

## 9. Performance & Development Roadmap

### 9.1 Performance Notes

The simulation is optimized for real-time or near real-time operation on standard machines.

### 9.2 Future Work

- Closed-loop PID and LQR control modules  
- GUI frontend  
- Real-world flight data calibration  
- Extended axes (lateral-directional simulation)

---

## Appendix

For full source code, documentation, and UAV model definitions, visit the GitHub repository.
[Github](https://github.com/daglar510/UAV_flight_dynamics_simulator)

---

*Project by Dağlar Duman, 2025*
