# GuardianBot
**AI-Powered Smart Home Assistant & Security Robot**

* **Project Name:** GuardianBot
* **Project Category:** Smart Life Robotics
* **Development Platform:** D-Robotics RDK X5
* **Robot Platform:** MasterPi AI Vision Robot Arm with Mecanum Wheels
* **Development Focus:** Edge AI, Computer Vision, Mobile Robotics, Robotic Manipulation
* **Competition:** Robotics Dream Keeper Challenge

---

## 1. Project Overview

GuardianBot is a planned mobile indoor inspection robot built around the D-Robotics RDK X5 and MasterPi chassis. The Stage 3 baseline uses BPU person and object detection, CPU tracking, local event snapshots, and supervised low-speed Mecanum movement with a forward obstacle stop. The project is in Stage 2 design.

The [Stage 2 Proposal](docs/stage2/PROJECT_PROPOSAL.md) defines the demo scope and KPI targets. Autonomous waypoint patrol, arm-based camera adjustment, and a dashboard for event snapshots are optional extensions. Object pickup is future work.

## 2. Robot Capabilities

### 2.1 AI Vision
GuardianBot uses its camera paired with AI models to analyze the surrounding environment.

**Planned Capabilities:**
* **Person Detection:** Detect people within the monitored area.
* **Object Detection:** Detect and classify objects.
* **Object Tracking:** Track the positions of objects.
* **Scene Analysis:** Analyze the surrounding environment.
* **Event Detection:** Detect predefined events.
* **Evidence Capture:** Capture image evidence when an event occurs.

**Example Use Cases:**
* Detecting the presence of a person in an area.
* Detecting objects blocking a pathway.
* Detecting displaced or moved items.
* Capturing images of events requiring inspection.

> **Note:** Person detection does not imply personal identification. Facial recognition or identity verification is an additional function that requires careful consideration regarding privacy and security.

### 2.2 Autonomous Patrol
In the optional patrol extension, GuardianBot would navigate to predefined inspection checkpoints.

**Planned Capabilities:**
* Define inspection checkpoints (Waypoints).
* Navigate along designated routes.
* Monitor the environment while traveling.
* Check for obstacles along the path.
* Halt when an unsafe situation is encountered.
* Report operational status.

> **Stage 3 scope:** The baseline uses supervised low-speed Mecanum motion and a front obstacle stop. Autonomous waypoint patrol is an optional extension after motion, safe stopping, and position estimation are validated. SLAM and map generation are future work.

### 2.3 Forward Obstacle Stop

For the baseline demo, the front range sensor measures distance ahead. The motion supervisor stops or inhibits forward movement when the path is blocked or the reading is invalid or stale. Test lateral and reverse movement separately in a cleared area under supervision.

### 2.4 Robotic Arm

The MasterPi arm and gripper are listed in the kit inventory. The exact revision and joint count are pending confirmation on the physical unit. Camera angle adjustment is optional after verifying the servo interface and movement limits. Object pickup is future work.

### 2.5 Smart Event Monitoring

1. Capture and timestamp a camera frame.
2. Run detection on the RDK X5 BPU and track detections on the CPU.
3. When a configured event is confirmed, save the matching snapshot and timestamped metadata locally.

### 2.6 Dashboard & Notifications

An optional dashboard can show event snapshots, timestamps, and status. Raw camera frames stay on the robot for the Stage 3 baseline. Live video streaming is a separate future idea outside the current proposal and demo scope.

## 3. Working Principle

A nearby operator guides GuardianBot to a different viewpoint. The camera and perception pipeline can trigger a local event record when a selected class is consistently detected. In a separate forward approach test, the front range sensor prompts a controlled stop. The physical motor stop is independent of the RDK X5 software path.

See the [Stage 2 Architecture](docs/stage2/ARCHITECTURE.md) for the data flow, module responsibilities, compute allocation, and ROS 2 interfaces.

---

## 4. Hardware Architecture

### 4.1 Main Computing Unit — D-Robotics RDK X5
The RDK X5 serves as the primary computing unit of GuardianBot.

**Responsibilities:**
* Execute AI Vision processing
* Perform person and object detection
* Analyze camera video streams
* Process sensor data
* Process control commands
* Interface with the software stack
* Communicate with the robot controller

**Key Highlight:** Equipped with a dedicated BPU (Brain Processing Unit) for AI acceleration, enabling real-time Edge AI directly on the robot.

### 4.2 Robot Platform — MasterPi
MasterPi serves as the mechanical base for mobility and object manipulation.

**Components:**
* 4x Mecanum Wheels
* 4x TT Motors
* Robotic arm and gripper (revision and joint count pending confirmation)
* Stage 1 USB camera for the baseline; kit camera compatibility pending
* Apparent front ultrasonic module installed; exact model, wiring, and operation pending confirmation
* Raspberry Pi chassis host and expansion board marked TurboPi; revisions pending
* Battery System

### 4.3 Hardware Integration Concept

The Stage 1 USB camera connects to the RDK X5. The RDK X5 sends bounded drive requests to a separately validated actuator controller. Confirm the MasterPi board revision, logic levels, protocol, and power requirements before choosing a controller path. The [Engineering Plan](docs/stage2/ENGINEERING_PLAN.md) records the BOM and fallback options.

---

## 5. MasterPi Hardware Inventory

### 5.1 Existing Hardware
The project currently has two primary hardware sets available: **RDK X5** and **MasterPi**.

**A. MasterPi AI Vision Robot Arm with Mecanum Wheels**

| No. | Component | Quantity | Function |
| :--- | :--- | :---: | :--- |
| 1 | MasterPi Robotic Arm (Pre-assembled) | 1 | Pick up objects and adjust camera angles |
| 2 | Chassis Brackets | 2 | Mount and support the robot frame |
| 3 | Hiwonder expansion board marked TurboPi | 1 | Connect and control peripherals |
| 4 | Battery Box | 1 | House the batteries |
| 5 | Structural Blocks ($3 \times 3$ cm) | 3 | Structural assembly components |
| 6 | Mecanum Wheels | 4 | Enable omnidirectional movement |
| 7 | White Wheel Couplings | 4 | Connect motors to wheels |
| 8 | TT Motors | 4 | Drive the wheels |
| 9 | Lithium Batteries | 2 | Power supply |
| 10 | USB Cable | 1 | Connect devices |
| 11 | Battery Charger | 1 | Charge the batteries |
| 12 | Phillips Screwdriver | 1 | Assembly and maintenance |
| 13 | Nuts and Screws Set | 1 set | Fasten components |
| 14 | MicroSD Card Reader | 1 | Read and manage MicroSD cards |
| 15 | Raspberry Pi chassis host | 1 | Candidate host for the existing drive and sensor interfaces |

**B. D-Robotics RDK X5**

| Component | Quantity | Function |
| :--- | :---: | :--- |
| RDK X5 | 1 | AI processing and main system control |

> **Note:** The availability of a MicroSD Card, cooling system, and an appropriate power supply must be verified separately, as they are not confirmed in the provided inventory list.

---

## 6. Additional Hardware Requirements
This list covers potential supplementary components that may need to be procured and are not confirmed as currently on hand.

| Component | Purpose | Necessity |
| :--- | :--- | :--- |
| MicroSD Card | Operating system and data storage | Needs verification |
| Power Supply 5V/5A for RDK X5 | Power the main compute board | Requires appropriate power source |
| Motor Controller | Control drive motors | Check existing board first |
| Servo Controller | Control robotic arm servos | Check existing board first |
| Wheel Encoder | Measure wheel rotation and odometry | Recommended |
| IMU Sensor | Measure motion, orientation, and heading | Recommended |
| Additional Distance Sensor | Detect surrounding obstacles | Based on test results |
| Emergency Stop | Immediately halt the system in emergencies | Highly recommended |
| DC-DC Converter | Step-down/regulate voltage levels | Based on power design |
| Cooling Fan / Heatsink | Thermal dissipation | Check existing accessories first |

> **Note:** Before purchasing additional hardware, existing circuitry and control board capabilities must be inspected to avoid redundant procurement.

---

## 7. Software Architecture

### 7.1 Main Software

| Software / Framework | Role / Function |
| :--- | :--- |
| Python | Primary development language |
| Linux | Operating system |
| AI Model | Object and person detection/classification |
| OpenCV | Image processing |
| RDK AI SDK | Leverage hardware AI/BPU capabilities of RDK X5 |
| ROS 2 | Robotics communication and system orchestration |
| Git / GitHub | Source code management |
| Dashboard | Status visualization and event monitoring |

> **Note:** Compatible versions of Linux, ROS 2, and SDK supported by the RDK X5 must be verified prior to installation.

### 7.2 Software Modules

```text
GuardianBot/
│
├── perception/
│   ├── camera.py
│   ├── person_detection.py
│   ├── object_detection.py
│   └── object_tracking.py
│
├── navigation/
│   ├── waypoint.py
│   ├── mecanum_control.py
│   └── obstacle_avoidance.py
│
├── manipulation/
│   ├── arm_control.py
│   ├── servo_control.py
│   └── object_pickup.py
│
├── monitoring/
│   ├── event_detection.py
│   ├── evidence_capture.py
│   └── notification.py
│
├── dashboard/
│
├── config/
│
└── main.py
```

---

## 8. Stage 2: Build — Development Plan

- [Project Proposal](docs/stage2/PROJECT_PROPOSAL.md) for the concept, baseline and optional scope, and measurable targets.
- [Architecture](docs/stage2/ARCHITECTURE.md) for the data flow, compute plan, and ROS 2 interfaces.
- [Engineering Plan](docs/stage2/ENGINEERING_PLAN.md) for the BOM, five risks and fallback plans, and repository layout.
- [Roadmap](ROADMAP.md) for milestones through the final demo.

## 9. Risk Analysis

See the [Engineering Plan](docs/stage2/ENGINEERING_PLAN.md#five-main-risks) for the current risks, triggers, mitigations, and fallbacks.

## 10. Expected Outcomes

The Stage 3 demo is planned to show BPU detection with concurrent CPU tracking, a timestamped local event record, and supervised Mecanum movement with a controlled forward stop. The [Proposal](docs/stage2/PROJECT_PROPOSAL.md#9-measurable-success-targets-kpis) defines the targets to measure on the integrated robot.

## 11. Stage 2 Completion Checklist

The four design documents are published in the public project repository. The remaining items are confirming open hardware and BOM details and verifying the Stage 2 community permalink and Showcase PR. Track status in the [Stage 2 checklist](docs/stage2/CHECKLIST.md).

---

## 12. Project Development Direction
GuardianBot aims to integrate three core technological pillars:
1. **Edge AI:** Utilize the RDK X5 and its BPU for on-device image processing and environmental analysis.
2. **Mobile Robotics:** Utilize the MasterPi platform and Mecanum Wheels for omnidirectional indoor navigation.
3. **Robotic Manipulation:** Evaluate the arm for optional camera angle adjustment. Object handling is future work.

The ultimate goal is to develop an intelligent robot capable of perceiving, analyzing, deciding, navigating, and operating safely within a home environment.

---

* **Project Name:** GuardianBot
* **Platform:** D-Robotics RDK X5
* **Robot Base:** MasterPi AI Vision Robot Arm with Mecanum Wheels
* **Project Category:** Smart Life Robotics
* **Development Stage:** Stage 2 — Build

> *This document serves as the Project Design & Development Plan for GuardianBot, clearly distinguishing existing hardware on hand from proposed supplementary components, as well as separating planned development capabilities from verified test results.*