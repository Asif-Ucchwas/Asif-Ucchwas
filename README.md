<h1 align="center">Md Asifuzzaman</h1>
<h3 align="center">
<b>I build robotics and autonomous systems — planning, perception, controls, and the embedded/cloud plumbing underneath them.</b>
</h3>

<div align="center">
<span style="font-size:0.7em; font-weight:normal; display:inline-block; max-width:600px;">
My work so far has been on ground robots and automotive-adjacent systems (CAN bus, real-time control, functional safety) — I'm building toward autonomous vehicles and industrial robotics next.
</span>
</div>

<p align="center">
M.E.S. Electrical & Electronics Engineering, Lamar University (2026) · Beaumont, TX · open to relocating anywhere in the US
</p>

<p align="center">
📧 <a href="mailto:asifuzzamanucchwas@gmail.com">asifuzzamanucchwas@gmail.com</a> &nbsp;·&nbsp;
💼 <a href="https://linkedin.com/in/masifuzzaman">linkedin.com/in/masifuzzaman</a>
</p>

---

<div align="center">

| **9** | **1,010+** | **400** | **98%** |
|:---:|:---:|:---:|:---:|
| Live Repos | Benchmark Trials Run | Cross-Validation Tests, 0 Discrepancies | Best Planner Success Rate |

</div>

---

### The short version

My thesis planner beats RRT* by 5.87% on path length with a 98% success rate. That proved I could plan a path. The next question was whether I could build everything *around* it — perception, embedded networking, real-time control, cloud infrastructure, multi-agent coordination — the full stack a robot actually needs to move through the real world.

So I mapped out five pieces of that stack I hadn't built yet, and built each one as an independent project, from scratch. Nine repos below, all live, all with a `DEVLOG.md` documenting what actually broke along the way — not a highlight reel with the mistakes cut out.

**If you want to know whether I can actually build this or not — you need to read the DEVLOGs.**

---

## 🎬 One story, in full

**[MultiPlan](https://github.com/Asif-Ucchwas/multiplan)** is the project I'd point to first. It's a nonholonomic motion-planning and multi-agent coordination stack — Dubins curves, all 48 Reeds-Shepp path words, RRT* with Reeds-Shepp steering, wait-for-graph deadlock detection, and task allocation solved two independent ways (MILP and the Hungarian algorithm).

The interesting part isn't the feature list — it's what broke along the way. Two formula bugs turned up in Dubins curves I'd *already implemented once before*, from memory, in my thesis. That was the moment I stopped trusting hand-derivation and cross-validated the full 48-word Reeds-Shepp implementation against an independent reference across 400 automated tests — zero discrepancies, but only after finding two more optimization bugs in RRT* through deliberate multi-iteration testing (100 → 1000 iterations, checking that cost actually improved monotonically instead of trusting one lucky run).

Then I benchmarked the whole thing against my own published thesis planner — including the runs where the new system was *worse*. That comparison is in the repo, not just the wins.

---

## 🧭 Core Portfolio

| Project | What it proves | Verified by | Repo |
|---|---|---|---|
| **Percept-Nav** | I can fuse a camera and LiDAR and act on it in real time | Custom C++ Nav2 costmap plugin, stress-tested to 8 simultaneous moving obstacles at 4x speed — zero failures | [percept-nav](https://github.com/Asif-Ucchwas/percept-nav) |
| **CAN-Net** | I can talk the language of real vehicle hardware | Full J1939 protocol (PGN/SPN encoding, multi-packet BAM transport), Zephyr RTOS bridged to a live Linux CAN interface, 360-trial CAN/UDP/TCP benchmark | [can-net](https://github.com/Asif-Ucchwas/can-net) |
| **ControlLoop-RT** | I can design a controller *and* know when not to trust it | PID beat MPC on unconstrained tracking (6.06% vs 8.18% overshoot) — reported honestly. Fault-injection-tested safety fallback cut uncontrolled coast distance from 0.48 rad to 0.0000 rad | [controlloop-rt](https://github.com/Asif-Ucchwas/controlloop-rt) |
| **MultiPlan** | I can build planning algorithms from primary sources, not memory | 48/48 Reeds-Shepp words cross-validated, 400 automated tests, 0 discrepancies. Benchmarked directly against my own thesis planner | [multiplan](https://github.com/Asif-Ucchwas/multiplan) |
| **TelemOps** | I can ship the infrastructure a robot fleet actually runs on | Docker + Kubernetes + Terraform pipeline, load-tested to a measured ~9,700 frames/sec ceiling, proved PVC durability by killing and rebuilding the cluster | [telemops](https://github.com/Asif-Ucchwas/telemops) |
| **Hybrid A\*–RRT\*** | Where all of this started — my Master's thesis | 5.87% path-length improvement over RRT*, 98% vs 60% success rate across 50 trials; ported to live ROS2 nodes with Gazebo/Nav2/TurtleBot3; from-scratch Kalman filter (44.1% error reduction) | [hybrid-a-star-rrtstar-path-planning](https://github.com/Asif-Ucchwas/hybrid-a-star-rrtstar-path-planning) · [thesis (ProQuest)](https://www.proquest.com/dissertations-theses/obstacle-avoidance-optimal-path-planning/docview/32699575) |

**By the numbers:**

| Project | Headline Result |
|---|---|
| Percept-Nav | 8 simultaneous moving obstacles @ 4x speed, 0 failures |
| CAN-Net | 360-trial benchmark across 3 transports (CAN/UDP/TCP) |
| ControlLoop-RT | 0.48 → 0.0000 rad uncontrolled coast distance after redesign |
| MultiPlan | 400/400 cross-validation tests, 0 discrepancies |
| TelemOps | ~9,700 frames/sec measured throughput ceiling |
| Hybrid A\*–RRT\* | 5.87% shorter paths, 98% vs 60% success rate over RRT* |

---

## 🧰 What I can actually build with — the detailed toolkit

This is the detail a short bio can't hold. Every line below is something I built and can walk you through — not a buzzword picked up from somewhere else. Each one links back to the project where it's proven.

<details>
<summary><b>Motion Planning & Trajectory Optimization</b></summary>
<br>

- **A\*, RRT, RRT\*, PRM, DWA** — implemented as clean, independently tested modules; extended into a novel hybrid planner *(Hybrid A\*–RRT\*)*
- **Dubins & Reeds-Shepp nonholonomic curves** — all 6 Dubins primitives plus full 48-word Reeds-Shepp coverage, implemented from cited primary sources and cross-validated against an independent reference across 400 automated tests, zero discrepancies *(MultiPlan)*
- **Behavior trees / task planning** — full `py_trees` implementation with blackboard state sharing, fallback/recovery subtrees, verified on both success and forced-failure paths *(MultiPlan)*
- **Computational geometry** — Shapely/GEOS workspace modeling, visibility-graph construction, Dijkstra shortest path, with measured O(n²·m) scaling behavior *(MultiPlan)*
- **Multi-agent coordination & deadlock prevention** — priority-based conflict resolution and a formal wait-for-graph deadlock detector *(MultiPlan)*
- **Task allocation / operations research** — the linear assignment problem solved two independent ways (PuLP MILP and SciPy's Hungarian algorithm), cross-validated for exact agreement *(MultiPlan)*
- **Trajectory generation, kinematics & dynamics modeling, vehicle dynamics** — applied consistently across every planner benchmark

</details>

<details>
<summary><b>Perception & Sensing</b></summary>
<br>

- **OpenCV (classical computer vision)** — an adaptive-threshold obstacle detector, reached after iterating through 7 failed techniques with the full debugging journey documented *(Percept-Nav)*
- **Camera + LiDAR sensor fusion** — time-synchronized pinhole-camera projection fused with 360° LiDAR range data, verified tracking real distance as the robot moves *(Percept-Nav)*
- **SLAM (SLAM Toolbox)** — live occupancy mapping with a full save/reload cycle verified end-to-end *(Percept-Nav)*
- **Nav2 costmap plugin development in C++** — a custom `pluginlib` layer written from scratch, compiled and loaded live inside a running Nav2 stack *(Percept-Nav)*
- **Occupancy grid mapping & localization (AMCL / TF2)** — the localization backbone behind every live ROS2 demo in this portfolio

</details>

<details>
<summary><b>State Estimation & Controls</b></summary>
<br>

- **Kalman filtering** — built entirely from scratch (constant-velocity 2D model), 44.1% error reduction validated on synthetic data and confirmed on a live robot trajectory *(thesis extension)*
- **Classical control design (pole placement)** — diagnosed a real closed-loop instability via pole/System-Type analysis and redesigned it down to 6.06% overshoot *(ControlLoop-RT)*
- **PID & feedforward control (model inversion)** — 87.4% RMS tracking-error reduction, plus correctly identifying and documenting *when* feedforward gives zero benefit *(ControlLoop-RT)*
- **Model Predictive Control (do-mpc / CasADi)** — a constrained receding-horizon QP controller; found and reported honestly that PID actually beats MPC on unconstrained tracking *(ControlLoop-RT)*
- **Functional safety engineering** — an independent watchdog validated by fault injection (200/200 faults caught, 0 false positives) and a redesigned safe-state fallback *(ControlLoop-RT)*
- **Functional safety standards mapping (ISO 26262)** — a documented hazard analysis with a full traceability table from safety goal to measured verification evidence *(ControlLoop-RT)*
- **State-space modeling, LQR fundamentals** — the control-theory foundation behind the above

</details>

<details>
<summary><b>Embedded Systems & Networking</b></summary>
<br>

- **Real-time embedded systems (Zephyr RTOS)** — a genuine 1kHz periodic control task with verified interrupt-driven preemption and measured zero jitter under adversarial load *(ControlLoop-RT, CAN-Net)*
- **CAN bus / SocketCAN** — a virtual CAN interface with kernel-level ID filtering and bus contention/arbitration analysis *(CAN-Net)*
- **CAN tooling (DBC, cantools)** — wrote a DBC file from scratch and encoded/decoded real signals with correct scale/offset math *(CAN-Net)*
- **J1939 protocol** — real PGN/SPN signal encoding, manual 29-bit extended CAN ID bit-packing, multi-packet BAM transport for messages over 8 bytes, and a request/response diagnostic pattern *(CAN-Net)*
- **TCP/IP, UDP, Serial** — length-prefix framing, simulated packet loss/reorder via `tc`/`netem`, and a virtual serial link via `socat` *(CAN-Net)*
- **RTOS-to-Linux bridging** — Zephyr's native CAN driver bridged to a real Linux SocketCAN interface, genuine cross-system integration *(CAN-Net)*
- **ARM microcontrollers & hardware bring-up** — real-time embedded control loops on Arduino *(Smartphone-Controlled Surveillance Robot)*

</details>

<details>
<summary><b>Cloud, DevOps & Data Infrastructure</b></summary>
<br>

- **Docker & multi-stage builds** — containerized a live CAN data source with a measured, honestly-reported image-size reduction *(TelemOps)*
- **Docker Compose orchestration** — a 4-service stack with host networking for hardware-level SocketCAN access *(TelemOps)*
- **Kubernetes (minikube)** — full Deployments/Services/PVCs, diagnosed and fixed a real hostNetwork-vs-cluster-DNS conflict *(TelemOps)*
- **Terraform (Infrastructure as Code)** — converted a full Kubernetes manifest set into Terraform resources and proved a clean rebuild from configuration alone *(TelemOps)*
- **Data pipeline & schema design, write batching** — replaced row-at-a-time inserts with batched writes, load-tested to a measured ~9,700 frames/sec throughput ceiling *(TelemOps)*
- **Grafana dashboards & alerting** — live time-series panels with a threshold alert directly observed transitioning between states against real data *(TelemOps)*
- **CI/CD (GitHub Actions)** — a real pipeline running the full test suite on every push, verified in a clean venv before it ever shipped *(CAN-Net, portfolio-wide)*

</details>

<details>
<summary><b>Software Engineering Practices</b></summary>
<br>

- **Object-oriented design, design patterns, finite state machines, data structures & algorithms, system architecture**
- **Unit testing (pytest / gtest)** — real test suites written across the portfolio; caught two test suites that existed locally but had never actually been committed to git
- **Coverage analysis & honest reporting** — per-file breakdowns instead of one blended number, since forcing a single coverage metric onto RTOS timing or embedded C would misrepresent what's actually verified
- **Build system auditing (CMake, colcon, rosdep)** — cross-referenced declared dependencies against actual imports and found 10 genuinely undeclared ROS2 dependencies
- **Production logging & error handling, config externalization** — structured logging in place of `print()`, hardcoded constants moved to real ROS2 parameters and environment variables
- **Issue tracking (GitHub Projects v2)** — a real backlog with closed, evidence-linked bugs across the portfolio, not a demo shell
- **LLM-assisted / agentic tooling (Claude API)** — designed and shipped a standalone tool-calling agent, verified end-to-end through live API calls *(portfolio-agent)*

</details>

<details>
<summary><b>Testing, Validation & Benchmarking</b></summary>
<br>

- **Statistical benchmark design** — 600-trial and 360-trial protocols, fully specified before any data was collected *(ControlLoop-RT, CAN-Net)*
- **Structured test planning & execution, regression testing, automated test pipelines**
- **Rosbag-style data recording & replay**
- **Root-cause debugging** — diagnosing with direct evidence (closed-loop pole computation, independent bus-level measurement) instead of guess-and-restart, applied consistently across every project
- **Quantitative reporting & data visualization (NumPy, SciPy, Matplotlib)**

</details>

---

## 🤖 Tooling I built to support the portfolio itself

**[portfolio-agent](https://github.com/Asif-Ucchwas/portfolio-agent)** — a small Claude API tool-calling agent that reads real benchmark files and real GitHub issue state across the repos above and drafts grounded status reports. No mocked data: both tools were verified in isolation against real files before a single live API call. Built to prove I can build *with* agentic tooling, not to explain away how the rest of this portfolio was written — that distinction is documented explicitly in the repo.

---

## 🌱 Where it started

Before the portfolio approach, two earlier projects laid the groundwork:

**[Smartphone-controlled surveillance robot](https://github.com/Asif-Ucchwas/smartphone-controlled-surveillance-robot)** — 3rd place, national robotics competition, Bangladesh.
Embedded C++ on Arduino for real-time directional command parsing and motor-driver control logic; Bluetooth (HC-05) wireless communication integration; DC motor control and driver-circuit interfacing; hardware bring-up and debugging of real wireless/motor edge cases; full end-to-end embedded architecture designed solo, from Android app through Bluetooth to Arduino to motor driver to DC motors.

**[IoT transmission-line fault detection](https://github.com/Asif-Ucchwas/iot-transmission-line-fault-detection)** — co-authored, published in IJSRP, July 2023.
Sensor-based three-phase electrical fault detection and analysis; IoT sensor integration for real-time monitoring; data analysis and fault classification; technical research writing and peer-reviewed publication.

---

<p align="center"><i>Every number on this page has a benchmark file behind it. If something looks impressive, the DEVLOG will tell you what broke first.</i></p>
