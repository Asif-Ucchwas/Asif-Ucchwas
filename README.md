# Hi, I'm Asif 👋

### Robotics & Autonomous Systems Engineer

I build motion planning and navigation systems for autonomous mobile robots.
Recently completed my MES in Electrical & Electronics Engineering at Lamar University (May 2026),
where my thesis achieved a 5.87% path-length improvement over RRT* with 98% success rate across 50 trials.

---

## What I work on

- Motion planning algorithms — A*, RRT*, Hybrid planners
- ROS2 node development and Nav2 integration
- Kalman filter state estimation for robot pose tracking
- Gazebo simulation and TurtleBot3 navigation
- Autonomous vehicle planning and control systems
- Embedded networking & real-time CAN bus systems — SocketCAN, J1939, RTOS integration

---

## Key Skills

| Robotics | Embedded & Networking | Programming | Tools |
|----------|------------------------|-------------|-------|
| ROS2 Jazzy | SocketCAN / CAN bus | Python | Gazebo |
| Nav2 | J1939 (PGN/SPN, BAM transport) | C++ | Linux/Ubuntu |
| Motion Planning | Zephyr RTOS | Git/GitHub | WSL2 |
| TF2 / URDF | TCP/UDP/Serial | NumPy/Matplotlib | LaTeX |
| Kalman Filter | DBC / cantools | | Docker |

---

## Featured Projects

### Hybrid A*-RRT* Path Planner

My MES thesis — a hybrid motion planning algorithm for autonomous mobile robots.

- 5.87% path-length improvement over RRT*
- 98% success rate across 50 simulation trials
- Tested at obstacle densities: 0.10, 0.20, 0.30
- Optimization index: J = aL + bT + g(1-S)
- Ported to ROS2 (Jazzy), tested live with Nav2/Gazebo/TurtleBot3 using real map + TF2 localization data
- Added Kalman filter state estimation (new contribution): 44.1% error reduction validated on synthetic data, confirmed live tracking a real robot trajectory
- Independent 50-trial reproducibility benchmark included in repo

[View Repository](https://github.com/Asif-Ucchwas/hybrid-a-star-rrtstar-path-planning) | [View Thesis on ProQuest](https://www.proquest.com/dissertations-theses/obstacle-avoidance-optimal-path-planning/docview/32699575)

---

### CAN-Net: Embedded Networking & Real-Time CAN Bus Communication Stack

A from-scratch embedded networking stack — TCP/UDP/Serial foundations, SocketCAN, the J1939 automotive protocol, and RTOS integration — built entirely in software/emulation.

- Real J1939 signal encoding (PGN/SPN) and multi-packet BAM transport for messages exceeding CAN's 8-byte limit
- Zephyr RTOS bridged to a real Linux CAN interface, with timestamped proof of preemptive scheduling
- 360-trial benchmark comparing CAN vs UDP vs TCP under varying load, with documented methodology and an honest analysis of what the results do and don't mean
- Independent of thesis work — built to close a specific embedded/networking skill gap

[View Repository](https://github.com/Asif-Ucchwas/can-net)

---

### IoT-Based Fault Detection System

Co-authored research paper — sensor fusion for industrial fault detection.
Published: IJSRP, July 2023

### Smartphone-Controlled Mobile Robot

Arduino-based robot with wireless control interface.
3rd place — national robotics competition, Bangladesh

---

## Currently

- Open to robotics engineering roles (motion planning, autonomy, AV)
- Deployed A*, RRT*, and Hybrid planners as ROS2 nodes, tested live against Gazebo/Nav2 simulation
- On F-1 STEM OPT — no sponsorship required (36 months)
- Open to relocation anywhere in the US

---

## Contact

- LinkedIn: https://linkedin.com/in/masifuzzaman
- Email: asifuzzamanucchwas@gmail.com
- Location: Beaumont, TX (open to relocation)
