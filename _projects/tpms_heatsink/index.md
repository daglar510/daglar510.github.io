---
layout: post
title: "TPMS Heat Sink Design Trade Study — Gyroid vs Schwarz-D (1-CPU & 2-CPU) | MTH450"
description: >-
  TPMS lattice heat sink trade study comparing Gyroid and Schwarz-D for 1-CPU and 2-CPU thermal loads.
  Built analytical thermal-resistance networks + MATLAB sizing model and validated with Fusion 360 flow/thermal simulations
  under natural vs forced convection.
skills:
  - Heat Transfer
  - Thermal Resistance Networks
  - Thermal Design
  - Fusion 360 Simulation (Thermal/Flow)
  - MATLAB
  - CAD Modeling
  - Engineering Trade Studies
main-image: /assets/img/tpms_heatsink/tpms_heatsink_header.png
date: 2026-01-13
---

## Overview
This project evaluates **TPMS (Triply Periodic Minimal Surface)** lattice heat sinks—**Gyroid** and **Schwarz-D**—for electronics cooling under two operating configurations:

- **1-CPU:** single heat source
- **2-CPU:** dual heat sources sharing the same copper/spreader → heat sink path

I used an industry-style workflow:
1) **First-pass design** with **thermal resistance networks** and a **MATLAB model**  
2) **Validation** with **Fusion 360 thermal + flow** simulations (natural vs forced convection)  
3) **Decision** using clear **Pass / Fail** outcomes

{% include image-gallery.html images="/assets/img/tpms_heatsink/tpms_heatsink_header.png" height="360" %}

---

## Project Files
- [Download Full Report (PDF)](/assets/pdf/tpms_heatsink/mth450_tpms_heatsink_report.pdf)
- [Download MATLAB Model (.m)](/assets/code/tpms_heatsink/tpms_heat_sink_model.m)

---

## Design Logic 
At a high level, the temperature rise is governed by:

- **Conduction path**: junction → chip/package → TIM → copper/spreader → TIM → heat sink base → lattice body  
- **Convection path**: lattice surface → ambient air (**this becomes the bottleneck without a fan**)

Instead of relying only on CFD visuals, the resistance network makes the dominant limiter obvious:
- with **low airflow** → **R_fin,conv** dominates → temperatures explode  
- with **forced airflow** → convection improves → lattice geometry and effective surface area become meaningful

The thermal budget is set by a maximum allowed junction temperature:

$$
T_{j,max} = 85^\circ C,\quad T_{amb} = 35^\circ C \Rightarrow \Delta T_{budget} = 50^\circ C
$$

A scenario is marked:
- **Pass** if max component temperature stays within the limit
- **Fail** if it exceeds the limit

---

## Thermal Resistance Networks (Correct topologies)

### 1-CPU Network (series path: $T_j \rightarrow T_{ambient}$)

<!-- 1-CPU Network (Tj -> Tambient) -->
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1600 200" style="width:100%; height:auto; display:block;">
  <defs>
    <style>
      .w{stroke:#1f3b86;stroke-width:4;fill:none;stroke-linecap:round;stroke-linejoin:round}
      .t{font-family:Arial,sans-serif;fill:#1f3b86;font-weight:700}
      .l{font-family:Arial,sans-serif;fill:#1f3b86;font-weight:600}
    </style>
  </defs>

  <text class="t" x="40" y="120" font-size="26">T_j</text>
  <text class="t" x="1515" y="120" font-size="26">T_ambient</text>

  <!-- lead-in -->
  <path class="w" d="M95 110 L175 110"/>

  <!-- R_chip -->
  <path class="w" d="M175 110
                      L195 110 L205 90 L225 130 L245 90 L265 130 L285 90 L305 130 L325 90 L335 110 L345 110"/>
  <text class="l" x="240" y="70" font-size="20">R_chip</text>
  <path class="w" d="M345 110 L395 110"/>

  <!-- R_TIM_CPU -->
  <path class="w" d="M395 110
                      L415 110 L425 90 L445 130 L465 90 L485 130 L505 90 L525 130 L545 90 L555 110 L565 110"/>
  <text class="l" x="430" y="70" font-size="20">R_TIM_CPU</text>
  <path class="w" d="M565 110 L615 110"/>

  <!-- R_Copper -->
  <path class="w" d="M615 110
                      L635 110 L645 90 L665 130 L685 90 L705 130 L725 90 L745 130 L765 90 L775 110 L785 110"/>
  <text class="l" x="655" y="70" font-size="20">R_Copper</text>
  <path class="w" d="M785 110 L835 110"/>

  <!-- R_TIM_HS -->
  <path class="w" d="M835 110
                      L855 110 L865 90 L885 130 L905 90 L925 130 L945 90 L965 130 L985 90 L995 110 L1005 110"/>
  <text class="l" x="870" y="70" font-size="20">R_TIM_HS</text>
  <path class="w" d="M1005 110 L1055 110"/>

  <!-- R_HS -->
  <path class="w" d="M1055 110
                      L1075 110 L1085 90 L1105 130 L1125 90 L1145 130 L1165 90 L1185 130 L1205 90 L1215 110 L1225 110"/>
  <text class="l" x="1110" y="70" font-size="20">R_HS</text>
  <path class="w" d="M1225 110 L1275 110"/>

  <!-- R_fin,conv -->
  <path class="w" d="M1275 110
                      L1295 110 L1305 90 L1325 130 L1345 90 L1365 130 L1385 90 L1405 130 L1425 90 L1435 110 L1445 110"/>
  <text class="l" x="1310" y="70" font-size="20">R_fin,conv</text>

  <!-- lead-out -->
  <path class="w" d="M1445 110 L1505 110"/>
</svg>



**Network meaning (1-CPU):** all resistances are in **series**, so:
$$
T_j - T_{ambient} = Q \cdot \left(R_{chip}+R_{TIM,CPU}+R_{Copper}+R_{TIM,HS}+R_{HS}+R_{fin,conv}\right)
$$

> Note: $R_{fin,conv}$ is the convection resistance from fin/lattice surface to ambient.


---

### 2-CPU Network (two sources merge into shared copper/spreader path)

<!-- 2-CPU Network (two sources merge into shared path) -->
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1600 320" style="width:100%; height:auto; display:block;">
  <defs>
    <style>
      .w2{stroke:#2b2b2b;stroke-width:4;fill:none;stroke-linecap:round;stroke-linejoin:round}
      .t2{font-family:Arial,sans-serif;fill:#2b2b2b;font-weight:700}
      .l2{font-family:Arial,sans-serif;fill:#2b2b2b;font-weight:600}
      .n{fill:#2b2b2b}
    </style>
  </defs>

  <text class="t2" x="40" y="55" font-size="26">2-CPU</text>

  <text class="t2" x="55" y="120" font-size="20">Tj1</text>
  <text class="t2" x="55" y="240" font-size="20">Tj2</text>

  <!-- TOP branch -->
  <path class="w2" d="M120 110 L200 110"/>
  <path class="w2" d="M200 110
                       L220 110 L230 90 L250 130 L270 90 L290 130 L310 90 L330 130 L350 90 L360 110 L370 110"/>
  <text class="l2" x="230" y="80" font-size="18">R_TIM,CPU</text>
  <path class="w2" d="M370 110 L470 110"/>

  <!-- BOTTOM branch -->
  <path class="w2" d="M120 230 L200 230"/>
  <path class="w2" d="M200 230
                       L220 230 L230 210 L250 250 L270 210 L290 250 L310 210 L330 250 L350 210 L360 230 L370 230"/>
  <text class="l2" x="230" y="200" font-size="18">R_TIM,CPU</text>
  <path class="w2" d="M370 230 L470 230"/>

  <!-- Merge -->
  <path class="w2" d="M470 110 L560 170"/>
  <path class="w2" d="M470 230 L560 170"/>
  <circle class="n" cx="560" cy="170" r="8"/>
  <text class="t2" x="580" y="176" font-size="18">T_copper</text>

  <!-- Shared path -->
  <path class="w2" d="M568 170 L640 170"/>

  <!-- R_Copper -->
  <path class="w2" d="M640 170
                       L660 170 L670 150 L690 190 L710 150 L730 190 L750 150 L770 190 L790 150 L800 170 L810 170"/>
  <text class="l2" x="690" y="140" font-size="18">R_Copper</text>
  <path class="w2" d="M810 170 L860 170"/>

  <!-- R_TIM,HS -->
  <path class="w2" d="M860 170
                       L880 170 L890 150 L910 190 L930 150 L950 190 L970 150 L990 190 L1010 150 L1020 170 L1030 170"/>
  <text class="l2" x="900" y="140" font-size="18">R_TIM,HS</text>
  <path class="w2" d="M1030 170 L1080 170"/>

  <!-- R_HS -->
  <path class="w2" d="M1080 170
                       L1100 170 L1110 150 L1130 190 L1150 150 L1170 190 L1190 150 L1210 190 L1230 150 L1240 170 L1250 170"/>
  <text class="l2" x="1145" y="140" font-size="18">R_HS</text>

  <!-- T_surface node -->
  <path class="w2" d="M1250 170 L1290 170"/>
  <circle class="n" cx="1290" cy="170" r="6"/>
  <text class="t2" x="1260" y="205" font-size="18">T_surface</text>

  <!-- R_fin,conv -->
  <path class="w2" d="M1290 170 L1330 170"/>
  <path class="w2" d="M1330 170
                       L1350 170 L1360 150 L1380 190 L1400 150 L1420 190 L1440 150 L1460 190 L1480 150 L1490 170 L1500 170"/>
  <text class="l2" x="1365" y="140" font-size="18">R_fin,conv</text>

  <!-- lead to ambient -->
  <path class="w2" d="M1500 170 L1540 170"/>
  <text class="t2" x="1550" y="176" font-size="20">T_amb</text>
</svg>

**Network meaning (2-CPU):**
- each CPU has its own local interface resistance into the copper/spreader region  
- both heat flows then share the downstream path (**R_Copper → R_TIM,HS → R_HS → R_fin,conv → ambient**)  
This coupling is why **2-CPU** is the real stress test.

---

## Analytical Summary (from the MATLAB sizing model)
The MATLAB model uses the above networks with:
- **effective convection area** (from CAD)
- **conduction resistances** (layer thickness, k, contact areas)
- and solves for the **minimum required convection coefficient \(h_{min}\)** to remain within the allowed temperature rise budget.

This is what the summary dashboard captures:


{% include image-gallery.html images="/assets/img/tpms_heatsink/tpms_summary_dashboard.png" height="800" %}


---

## Fusion 360 Validation (Flow + Thermal)
I validated the trade study using Fusion 360 by comparing:
- airflow penetration / flow-lines
- maximum component temperature (peak anywhere in the solid)

### Natural Convection (No Fan) — **Fail** cases
Low airflow (≈0.25–0.28 m/s) makes convection the limiting resistance (**R_fin,conv dominates**). Both geometries overheat.

**Gyroid — 1 CPU (No Fan): Fail**  
(0.25 m/s, 165.614°C)
{% include image-gallery.html images="/assets/img/tpms_heatsink/gyroid_1cpu_nofan.png" height="340" %}

**Schwarz-D — 1 CPU (No Fan): Fail**  
(0.27 m/s, 161.853°C)
{% include image-gallery.html images="/assets/img/tpms_heatsink/schwarz_1cpu_nofan.png" height="340" %}

**Gyroid — 2 CPU (No Fan): Fail**  
(0.28 m/s, 191.817°C)
{% include image-gallery.html images="/assets/img/tpms_heatsink/gyroid_2cpu_nofan.png" height="340" %}

**Schwarz-D — 2 CPU (No Fan): Fail**  
(0.26 m/s, 199.002°C)
{% include image-gallery.html images="/assets/img/tpms_heatsink/schwarz_2cpu_nofan.png" height="340" %}

---

### Forced Convection (With Fan) — **Pass** cases
With forced airflow, convection resistance drops significantly and the lattices become viable heat sinks. Here the geometry differences show up as **thermal margin**.

**Gyroid — 1 CPU (With Fan): Pass**  
(20.20 m/s, 47.274°C)
{% include image-gallery.html images="/assets/img/tpms_heatsink/gyroid_1cpu_with_fan.png" height="340" %}

**Schwarz-D — 1 CPU (With Fan): Pass**  
(24.03 m/s, 46.629°C)
{% include image-gallery.html images="/assets/img/tpms_heatsink/schwarz_1cpu_with_fan.png" height="340" %}

**Gyroid — 2 CPU (With Fan): Pass**  
(19.16 m/s, 79.316°C)
{% include image-gallery.html images="/assets/img/tpms_heatsink/gyroid_2cpu_with_fan.png" height="340" %}

**Schwarz-D — 2 CPU (With Fan): Pass**  
(19.15 m/s, 54.811°C)
{% include image-gallery.html images="/assets/img/tpms_heatsink/schwarz_2cpu_with_fan.png" height="340" %}

---

## Results Table 

<table>
  <thead>
    <tr>
      <th>Scenario</th>
      <th>Geometry</th>
      <th>Cooling</th>
      <th style="text-align:right;">Max Air Velocity (m/s)</th>
      <th style="text-align:right;">Max Component Temp (°C)</th>
      <th>Result</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>1 CPU</td><td>Gyroid</td><td>No Fan</td><td style="text-align:right;">0.25</td><td style="text-align:right;">165.614</td><td>Fail</td></tr>
    <tr><td>1 CPU</td><td>Gyroid</td><td>With Fan</td><td style="text-align:right;">20.20</td><td style="text-align:right;">47.274</td><td>Pass</td></tr>

    <tr><td>1 CPU</td><td>Schwarz-D</td><td>No Fan</td><td style="text-align:right;">0.27</td><td style="text-align:right;">161.853</td><td>Fail</td></tr>
    <tr><td>1 CPU</td><td>Schwarz-D</td><td>With Fan</td><td style="text-align:right;">24.03</td><td style="text-align:right;">46.629</td><td>Pass</td></tr>

    <tr><td>2 CPU</td><td>Gyroid</td><td>No Fan</td><td style="text-align:right;">0.28</td><td style="text-align:right;">191.817</td><td>Fail</td></tr>
    <tr><td>2 CPU</td><td>Gyroid</td><td>With Fan</td><td style="text-align:right;">19.16</td><td style="text-align:right;">79.316</td><td>Pass</td></tr>

    <tr><td>2 CPU</td><td>Schwarz-D</td><td>No Fan</td><td style="text-align:right;">0.26</td><td style="text-align:right;">199.002</td><td>Fail</td></tr>
    <tr><td>2 CPU</td><td>Schwarz-D</td><td>With Fan</td><td style="text-align:right;">19.15</td><td style="text-align:right;">54.811</td><td>Pass</td></tr>
  </tbody>
</table>
---

## Conclusions (Engineering Decision)
- **Without forced convection:** both lattices **fail** in both 1-CPU and 2-CPU configurations due to convection dominance (low airflow).
- **With forced convection:** both lattices **pass** for 1-CPU, but the 2-CPU case differentiates designs:
  - Gyroid passes with **smaller thermal margin** (79.316°C)
  - Schwarz-D passes with **large margin** (54.811°C)

**Final recommendation:** **Schwarz-D + forced convection** is the most robust configuration, especially under dual-source loading.

---

## What I personally did (ownership)
- Built the **correct 1-CPU and 2-CPU thermal resistance networks** and translated them into a solvable MATLAB model.
- Used CAD-derived effective areas to compute **convection sizing** (required \(h\) to meet the temperature rise budget).
- Ran and interpreted **Fusion 360 flow + thermal** results and tied the outcomes back to the resistance network physics.
- Produced a decision-ready trade study with clear Pass/Fail outcomes and supporting evidence.

---
