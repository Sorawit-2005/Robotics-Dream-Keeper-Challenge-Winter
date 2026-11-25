# GuardianBot
### AI-Powered Smart Home Assistant & Security Robot

**GuardianBot** is a smart mobile robotics project designed to explore the use of Edge AI, computer vision, and autonomous robotics for smart home assistance and security monitoring.

The project is being developed for the **RDK Winter Challenge**, using the D-Robotics RDK X5 as its main computing platform and the MasterPi AI Vision Robot Arm as its robotic platform.

> **Project Status:** Planning and system design  
> The Stage 2 design documents are published. Hardware compatibility checks and submission tracking are in progress.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Project Objectives](#project-objectives)
- [Planned Features](#planned-features)
- [Hardware Platform](#hardware-platform)
- [Software and Technologies](#software-and-technologies)
- [System Architecture](#system-architecture)
- [How It Is Expected to Work](#how-it-is-expected-to-work)
- [Development Roadmap](#development-roadmap)
- [Repository Structure](#repository-structure)
- [Project Documentation](#project-documentation)
- [Project Status](#project-status)
- [Developer](#developer)

---

## Project Overview

GuardianBot aims to develop an intelligent mobile robot that can assist with home monitoring, environmental observation, and basic object interaction.

The robot is designed around the **D-Robotics RDK X5**, which will serve as the main computing platform for AI inference and system processing.

The MasterPi platform provides the mobile chassis, Mecanum wheels, and robotic arm. These components will be integrated with the RDK X5 after hardware and software compatibility have been evaluated.

The long-term vision is to create a mobile robotic assistant capable of patrolling designated areas, detecting environmental events, avoiding obstacles, and interacting with selected objects.

## Project Objectives

1. Explore Edge AI applications using the D-Robotics RDK X5.
2. Design a mobile robot capable of navigating designated indoor areas.
3. Develop computer vision capabilities for environmental observation and object detection.
4. Investigate autonomous patrol and obstacle avoidance.
5. Integrate a robotic arm for controlled object manipulation and camera angle adjustment.
6. Design a web-based dashboard for monitoring robot status and recorded events.
7. Build a modular robotics architecture that can be expanded in future development stages.

## Planned Features

The following features are planned for development:

| Feature | Description |
|---|---|
| AI Vision | Run person and object detection on the RDK X5 BPU and tracking on the CPU. |
| Autonomous Patrol | Optional extension to navigate predefined waypoints after validating supervised motion and safe stopping. |
| Forward Obstacle Stop | Use the front range sensor to stop or inhibit forward movement. |
| Robotic Arm | Optional camera angle adjustment after hardware verification. Object pickup is future work. |
| Event Monitoring | Capture images and timestamps when configured events are detected. |
| Web Dashboard | Optional view of event snapshots and status. Raw camera frames stay on the robot in the baseline. |
| System Monitoring | Monitor operational information such as patrol state and battery status, subject to hardware support. |

**Development note:** Feature availability will depend on hardware integration, sensor availability, software implementation, and testing results.

## Hardware Platform

### Main Computing Platform

**D-Robotics RDK X5**

The RDK X5 is planned to serve as the robot's primary computing platform.

Its intended responsibilities include:

- AI inference and computer vision processing.
- Robot system coordination.
- Processing sensor information.
- Running the planned ROS 2 nodes for the Stage 3 baseline.
- Supporting an optional dashboard for event snapshots and status.

### Robotic Platform

**MasterPi AI Vision Robot Arm**

The MasterPi platform provides the robot's mechanical foundation.

The available kit includes:

| No. | Hardware Component | Quantity |
|---:|---|---:|
| 1 | MasterPi Robotic Arm | 1 |
| 2 | Chassis Mounting Brackets | 2 |
| 3 | Hiwonder expansion board marked TurboPi | 1 |
| 4 | Battery Holder | 1 |
| 5 | 3 cm × 3 cm Blocks | 3 |
| 6 | Mecanum Wheels | 4 |
| 7 | White Wheel Connectors | 4 |
| 8 | TT Motors | 4 |
| 9 | Lithium Batteries | 2 |
| 10 | USB Cable | 1 |
| 11 | Battery Charger | 1 |
| 12 | Phillips Screwdriver | 1 |
| 13 | Nuts and Screws Set | 1 |
| 14 | MicroSD Card Reader | 1 |

**Important hardware integration consideration**

The assembled chassis has a Raspberry Pi under an expansion board marked TurboPi. The exact board revisions and host link to the RDK X5 are pending verification. See the [port inventory](docs/stage2/ENGINEERING_PLAN.md#port-inventory).

Before connecting the hardware, the project will evaluate GPIO pin mapping, voltage levels, motor control interfaces, servo control, communication interfaces, and power requirements.

Additional components may be required depending on the final integration design.

## Software and Technologies

The following technologies are planned for the project:

| Technology | Intended Purpose |
|---|---|
| Python | AI applications, computer vision, and system logic |
| C++ | Performance-oriented robotics components |
| ROS 2 | Planned robotics middleware and modular communication |
| OpenCV | Image processing and computer vision |
| RDK AI SDK | Access to supported AI acceleration capabilities |
| Linux | Main development and runtime environment |
| Web Technologies | Web-based monitoring dashboard |
| Git & GitHub | Version control and project documentation |

Software versions, library compatibility, and supported development environments will be determined during the implementation phase.

## System Architecture

The RDK X5 BPU runs person and object detection. Its CPU handles tracking, event rules and motion supervision using ROS 2. The actuator controller handles motor I/O and the controller watchdog. The physical stop acts on the motor drive inhibit or power cutoff independently of the RDK X5.

See the [Architecture](docs/stage2/ARCHITECTURE.md) for the data flow and interfaces.

## How It Is Expected to Work

1. A nearby operator guides the robot at low speed to inspect a different viewpoint.
2. The camera feeds onboard detection and tracking. A confirmed event saves a snapshot and timestamp locally.
3. In the forward obstacle test, the front range sensor prompts the motion supervisor to stop or inhibit forward movement. Lateral and reverse tests use a cleared area.

Waypoint patrol, arm-based camera adjustment, and dashboard alerts are optional extensions.

## Development Roadmap

The [Roadmap](ROADMAP.md) lists the Stage 2 submission milestones and the Stage 3 integration, benchmark, and demo dates.

## Repository Structure

The Stage 1 report and evidence are in `stages/state 1/`. Stage 2 deliverables are in `docs/stage2/` and the root `ROADMAP.md`. The [Engineering Plan](docs/stage2/ENGINEERING_PLAN.md#planned-github-structure) lists the planned Stage 3 directories.

## Project Documentation

- **[Stage 1 Report](stages/state%201/STAGE1_IGNITE.md)** — Board bring-up, camera test, and YOLO evidence.
- **[Stage 2 Proposal](docs/stage2/PROJECT_PROPOSAL.md)** · [Architecture](docs/stage2/ARCHITECTURE.md) · [Engineering Plan](docs/stage2/ENGINEERING_PLAN.md)
- **[Stage 2 Checklist](docs/stage2/CHECKLIST.md)** — Task checklist, current progress, and proposed repository layout.

Additional project documentation will be maintained in the repository:

- **[GUARDIANBOT_PROJECT.md](GUARDIANBOT_PROJECT.md)** — Detailed project concept, hardware inventory, planned capabilities, and engineering considerations.
- **[ROADMAP.md](ROADMAP.md)** — Development milestones and project progress.
- **docs/** — System architecture, engineering plans, and supporting documentation.
- **`evidence/stage3/`** — Planned location for integration and benchmark evidence.

## Project Status

**Current stage: Stage 2 — Build.** The Proposal, Architecture, Engineering Plan, and Roadmap are public. Hardware details, the community post, and the Showcase PR remain to be confirmed. See the [Stage 2 checklist](docs/stage2/CHECKLIST.md) for current status.

## Developer

**Sorawit Namwongsa**

Kasetsart University  
Chalermphrakiat Sakonnakhon Province Campus

**Project:** GuardianBot  
**Competition:** RDK Winter Challenge

---

## Acknowledgements

This project is developed using the D-Robotics RDK X5 platform and MasterPi robotic hardware.

Special thanks to the communities and developers who contribute to open-source robotics, AI, and computer vision technologies.

---

*GuardianBot — Building an intelligent robotic assistant for smarter and safer living.*