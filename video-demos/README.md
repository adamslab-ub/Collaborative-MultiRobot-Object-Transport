# R2P2: Multi-Robot Box Transport Demo

> **Roles with Rules and Proportional-control Primitive** — a decentralized task and motion planning framework for collaborative box transport across flat, uphill, and downhill terrain.

---

## What You'll See in the Video

The video walks through five sections:

### 1. Introduction
A brief overview of the problem: multiple robots must collaboratively push a box from a start location to a goal, passing through intermediate waypoints — across surfaces with varying inclination and friction.

### 2. The R2P2 Framework
R2P2 decomposes the problem into **task planning** (role allocation) and **motion planning** (velocity control):

- **Role Assignment** — Each robot is assigned one of three roles based on the current box maneuver (rotation or translation) and the robot's position relative to the box:
  - **Push** — drives the box toward the goal
  - **Prevent** — resists excessive speed or undesired rotation
  - **Support** — prevents the box from slipping out of formation

- **Velocity Control** — Push robots use proportional control; Prevent and Support robots use rule-based velocity tracking of the box state.

- **Relocation Maneuver** — When robots drift from their desired positions during execution, they autonomously reposition themselves perpendicular to the box edge.

Key properties of R2P2:
- Fully **decentralized** — each robot makes its own decisions onboard
- **Generalizable** — same heuristic parameters work across different terrains, friction coefficients, and box weights

### 3. Simulation Results (NVIDIA IsaacSim)
Video contains R2P2 tests in a high-fidelity simulator across:

| Terrain | Robot Team Size |
|---------|----------------|
| Flat | 6 robots |
| Downhill (5°) | 6 robots |
| Uphill (5°) | 6 robots |
| Flat | 10 robots |
| Downhill (5°) | 10 robots |
| Uphill (5°) | 10 robots |

The simulation also demonstrates generalizability across friction coefficients (µ = 0.001, 0.01, 0.1) and box masses (0.5 kg, 2 kg, 6 kg).

### 4. Physical Experiment
R2P2 is validated on real hardware using **4 TurtleBot3 Burger robots** pushing a 1.2 kg cardboard box (1.2 m × 0.22 m × 0.21 m).

**Setup:**
- Localization via Motion Capture (MoCap) at 40 Hz
- Onboard compute: Raspberry Pi 4 Model B per robot
- Software: ROS2, with R2P2 running independently on each robot

**Mission path:** Start → Waypoint 1 (with ~40° clockwise rotation) → ~120° counter-clockwise rotation → Goal

The robots successfully transport the box through the full waypoint sequence.

### 5. Simulation vs. Real-World Comparison
The final section overlays the box trajectory from simulation and the physical experiment side by side.

**Key observations:**
- Overall trajectories are very similar between sim and real
- Minor deviations in curvature during straight motion (real-world)
- Some centroid drift during rotation (real-world) vs. pure rotation (simulation)
- Execution time: ~3 min (simulation) vs. ~22 min (real world), due to actuation limits, communication delays, and positioning inaccuracies not fully captured in simulation

---

## Paper Summary

**R2P2** assigns robots to Push, Prevent, or Support roles using simple geometric rules — no black-box learning, no centralized coordinator, and no real-time optimization. Our approach outperforms the Virtual Leader-Follower (VLF) baseline in all tested bearing angles (15°, 30°, 45°, 60°) across flat, uphill, and downhill terrain.

```
Authors: Aditya Bhatt, Himavarshini Yarragangu, Urvish Shah,
         Venkata Sai Yaswanth Mohan Thota, Souma Chowdhury
Institution: University at Buffalo — Dept. of Mechanical and Aerospace Engineering
Venue: ASME IDETC-CIE 2026, Houston, TX
Paper ID: IDETC2026-194231
```

---

## Citation

Under Review

---

*Supported by NSF Award CMMI 2048020. Facilities support from the University at Buffalo's Center for Embodied Autonomy and Robotics (CEAR).*