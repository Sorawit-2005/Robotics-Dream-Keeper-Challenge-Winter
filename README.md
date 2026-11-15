# GuardianBot
### AI-Powered Smart Home Assistant & Security Robot

**GuardianBot** is a smart mobile robotics project designed to explore the use of Edge AI, computer vision, and autonomous robotics for smart home assistance and security monitoring.

The project is being developed for the **RDK Winter Challenge**, using the D-Robotics RDK X5 as its main computing platform and the MasterPi AI Vision Robot Arm as its robotic platform.

> **Project Status:** Planning and system design  
> This project is currently in the hardware preparation and system design phase. The features described below represent the planned capabilities and development goals, not completed or validated functionality.

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
| AI Vision | Use computer vision and AI models to detect people and objects. |
| Autonomous Patrol | Navigate predefined patrol points (waypoints). |
| Obstacle Avoidance | Detect obstacles and plan appropriate movement responses. |
| Robotic Arm | Manipulate selected objects and adjust the camera viewing angle. |
| Event Monitoring | Capture images and timestamps when configured events are detected. |
| Web Dashboard | Provide a web interface for monitoring robot status and event history. |
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
- Communication with the dashboard.
- Supporting future ROS 2 integration.

### Robotic Platform

**MasterPi AI Vision Robot Arm**

The MasterPi platform provides the robot's mechanical foundation.

The available kit includes:

| No. | Hardware Component | Quantity |
|---:|---|---:|
| 1 | MasterPi Robotic Arm | 1 |
| 2 | Chassis Mounting Brackets | 2 |
| 3 | Raspberry Pi 5 Expansion Board | 1 |
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

The MasterPi expansion board is designed for Raspberry Pi 5. Its compatibility with the D-Robotics RDK X5 has not yet been confirmed.

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

The planned system architecture consists of five major layers:

1. **Perception Layer**
   - Camera input.
   - Image processing.
   - Object and person detection.
   - Environmental observation.

2. **AI Processing Layer**
   - AI model inference on the RDK X5.
   - Visual information analysis.
   - Event detection.

3. **Robot Control Layer**
   - Movement control.
   - Waypoint patrol.
   - Obstacle response.
   - Robotic arm control.

4. **Communication Layer**
   - Robot-to-dashboard communication.
   - Status reporting.
   - Event data transmission.

5. **User Interface Layer**
   - Web dashboard.
   - Robot status monitoring.
   - Event history.
   - Camera viewing interface.

The architecture will be refined after hardware compatibility testing and the initial software implementation.

## How It Is Expected to Work

The planned operational workflow is:

1. **Environment Observation:** The camera and available sensors collect environmental information.
2. **AI Processing:** The RDK X5 processes visual information using supported AI models.
3. **Decision Making:** The robot evaluates the detected information and determines an appropriate response.
4. **Motion Control:** The robot follows predefined patrol points and responds to detected obstacles.
5. **Object Interaction:** The robotic arm may be used to manipulate selected objects or adjust the camera angle.
6. **Event Recording:** Configured events may trigger image capture and timestamp recording.
7. **Dashboard Monitoring:** Relevant robot information and event records are intended to be displayed through a web dashboard.

## Development Roadmap

| Phase | Development Activities | Status |
|---|---|---|
| Phase 1 | Project concept and system planning | In Progress |
| Phase 2 | Hardware preparation and compatibility evaluation | In Progress |
| Phase 3 | Robot assembly and hardware integration | Planned |
| Phase 4 | Basic motor and robotic arm control | Planned |
| Phase 5 | Camera integration and AI vision development | Planned |
| Phase 6 | Autonomous patrol and obstacle avoidance | Planned |
| Phase 7 | Event monitoring and web dashboard | Planned |
| Phase 8 | System integration, testing, and optimization | Planned |

## Repository Structure

The repository is intended to follow a modular structure:

```text
GuardianBot/
│
├── README.md
├── GUARDIANBOT_PROJECT.md
├── ROADMAP.md
│
├── docs/
│   ├── concept/
│   ├── architecture/
│   ├── engineering/
│   └── images/
│
├── src/
│   ├── ai/
│   ├── vision/
│   ├── navigation/
│   ├── control/
│   ├── robotic_arm/
│   └── dashboard/
│
├── models/
├── launch/
│
└── evidence/
    └── stage2/
```

The directory structure may evolve as development progresses.

## Project Documentation

Additional project documentation will be maintained in the repository:

- **[GUARDIANBOT_PROJECT.md](GUARDIANBOT_PROJECT.md)** — Detailed project concept, hardware inventory, planned capabilities, and engineering considerations.
- **[ROADMAP.md](ROADMAP.md)** — Development milestones and project progress.
- **docs/** — System architecture, engineering plans, and supporting documentation.
- **evidence/** — Development photos, test results, and project evidence.

## Project Status

**Current Stage: Hardware Preparation and System Design**

Current activities:

- Defining the project concept and objectives.
- Preparing the D-Robotics RDK X5 and MasterPi hardware.
- Planning hardware integration.
- Designing the software architecture.
- Evaluating the technologies required for implementation.

The robot's planned capabilities will be updated as individual modules are implemented and tested.

## Developer

**Sorawit**

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