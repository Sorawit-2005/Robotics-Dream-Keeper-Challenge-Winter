# Project Proposal: GuardianBot — AI-Powered Smart Home Assistant & Security Robot

- **Project Name:** GuardianBot
- **Category:** Smart Life Robotics
- **Compute Platform:** D-Robotics RDK X5 (Edge AI / BPU)
- **Robot Base:** MasterPi AI Vision Robot Arm with Mecanum Wheels
- **Developer:** Sorawit Namwongsa (Computer Science, Kasetsart University Chalermphrakiat Sakonnakhon Province Campus)

---

## 1. Problem Statement & Concept

A fixed camera covers a single viewpoint. If furniture or a corner hides part of an indoor area, a household member may need to inspect that spot in person or install another camera. Continuous video can also make it difficult to find the moment that matters.

**GuardianBot** is a mobile indoor inspection robot designed to give a household member a second viewpoint and a short record of what the robot saw. A nearby operator guides the MasterPi chassis at low speed. Its USB camera sends frames to the D-Robotics RDK X5, where the BPU runs person and object detection and the CPU tracks detections across frames. A configured event saves a timestamped snapshot locally. Separately, a front range sensor can stop forward motion if the path is blocked.

The Stage 3 baseline demonstrates supervised movement, local AI and event capture, and a controlled forward stop. Waypoint patrol, arm-based camera inspection, and dashboard alerts are optional extensions.

## 2. Operating Scenario & Constraints

The representative demo takes place on a level indoor floor in a clear hallway or living-room test area. A nearby operator guides the robot toward a spot outside the simulated fixed-camera view. A consenting participant appears in the camera view, allowing the robot to detect and track a person and save a local event record. In a separate test, the operator approaches a stationary test obstacle and verifies that the robot stops with clearance.

- **Operating area:** Use a dry, flat floor under suitable indoor lighting. Verify wheel clearance and keep people clear of the robot's motion path.
- **Movement:** Forward approach is the obstacle-stop test. Test lateral or reverse movement separately in a cleared area because the front range sensor covers the forward direction.
- **Privacy:** Process raw frames on the robot. Keep event snapshots and metadata local for the baseline demo. Person detection identifies a class, without identifying individuals.
- **Hardware readiness:** Enable drive only after verifying the controller, front range sensor, power supply, and stop behavior. The arm stays out of the baseline scope. Its kit revision and joint count are pending verification.

## 3. Intended Users & Interaction Model

The primary user is a household member or family caregiver who wants to check a specific indoor area and review a record of what the robot saw. The baseline interaction assumes the user is present and can stop the robot. Remote review is an optional extension.

1. The operator enables drive in a cleared area and guides GuardianBot toward the inspection point.
2. The operator observes the robot while it runs detection and tracking. A configured rule can confirm an event when a target class, such as a person, is consistently detected across frames.
3. A blocked forward path or invalid range reading stops or inhibits forward movement. After a latched fault, the operator checks the area and re-enables drive once the fault clears. After the inspection, the operator reviews the saved snapshot and timestamp.

## 4. Hardware Compatibility & Power Architecture

- **Hardware Compatibility:**
  - The RDK X5 will operate as the primary computing platform, while the MasterPi expansion board will provide low-level hardware control where compatible.
  - Communication interfaces, motor drivers, servo controllers, and electrical compatibility must be verified before hardware integration.
  - The MasterPi expansion board is originally designed for Raspberry Pi platforms.
  - Direct compatibility with the RDK X5 has not yet been confirmed.

- Hardware interfaces and control protocols will be inspected before integration.
- The first integration option is to retain the installed Raspberry Pi and TurboPi-marked expansion board for chassis I/O, with a verified link to the RDK X5. A compatible external controller is the fallback.

- **Power Distribution Design**
  The power system will provide separate regulated power paths for the computing platform and high-current actuators.

- RDK X5: Dedicated regulated 5V power supply capable of delivering 5A.
- Motors: Dedicated motor power path compatible with the motor driver.
- Servos: Dedicated regulated servo power supply based on servo voltage and peak current requirements.

The power system will include appropriate voltage regulation, current protection, and common signal grounding where required.
All power connections will be verified before hardware integration.

## 5. Software & Communication Architecture

- **Software Architecture:**
  The software system will use Python and ROS 2 to organize AI perception, navigation, motor control, robotic arm control, and event monitoring.

  The RDK X5 will communicate with the MasterPi controller through a verified hardware communication interface.
  The communication protocol and ROS 2 hardware interface will be determined after inspecting the MasterPi expansion board.

  **Navigation Strategy**

  - **Stage 3 baseline:** The operator drives the robot at low speed in a controlled indoor area. The front range sensor can stop forward motion when an obstacle blocks the path.
  - **Optional waypoint patrol:** Once supervised movement and the stop interlock pass testing, evaluate autonomous travel between marked indoor checkpoints. Use calibrated odometry or another validated position estimate for control, and measure the final stop position against a floor reference. Pause patrol if the position estimate becomes unreliable or the path is blocked.
  - **Future work:** LiDAR SLAM and autonomous map generation.

## 6. Project Scope

| Priority | Features |
| --- | --- |
| Stage 3 baseline | Onboard person and selected object detection, tracking, local event logging, supervised Mecanum movement, and front obstacle stop |
| Optional extensions | Autonomous waypoint patrol, arm-based camera angle adjustment, dashboard, and remote notifications |
| Future work | Object pickup, LiDAR SLAM, and fall detection |

## 7. Core Capabilities

| Capability | What GuardianBot does in the baseline |
| --- | --- |
| Perception | The Stage 1 USB camera provides frames for detection and tracking. The planned front range sensor reports distance ahead once its interface has been verified. |
| Decision | The RDK X5 confirms configured events from tracked detections. It separately checks that drive is enabled and that the forward path and range data meet the motion rules. A detected person can trigger a record. A blocked forward path triggers a stop. |
| Actuation | The planned actuator controller drives the four Mecanum wheels within tested limits after hardware verification. It stops forward movement when requested by the supervisor. The event logger saves the matching snapshot and metadata locally. |

## 8. Innovation Compared with a Stock Demo

GuardianBot takes the detector beyond drawing boxes on a live image. The operator can bring the camera to a different viewpoint using the Mecanum chassis. On-device detection and tracking turn a sustained observation into a timestamped record the operator can review after the inspection. The front range sensor serves a separate purpose by protecting forward movement while the robot changes viewpoints.

The distinguishing contribution is the integration of mobile inspection, on-device AI, local event capture, and controlled stopping in one indoor workflow. If validated later, waypoint patrol and arm-based camera adjustment can extend how the robot reaches and inspects a viewpoint.

## 9. Measurable Success Targets (KPIs)

The demo should show a complete local event record for a configured detection and a separate forward obstacle test ending in a controlled stop. The numbers below are Stage 3 test targets. Record the measured values and test conditions after running the system.

### Baseline demo

| Metric | Target | How to measure |
| --- | ---: | --- |
| AI throughput | ≥ 25 FPS | Count processed frames per second through preprocessing, BPU inference, and postprocessing. Capture at 640 × 480 and record the model input size separately. |
| Obstacle clearance after stopping | ≥ 20 cm | Measure from the nearest point on the chassis to the obstacle at a full stop. Begin at low speed and test up to 0.2 m/s after validating safe stops. |
| Local event logging latency | < 500 ms | Time from event confirmation until the snapshot and timestamped metadata are written locally. |
| Detection precision | ≥ 85% | Evaluate per target class on held-out labeled indoor scenes. |
| Detection recall | ≥ 85% | Evaluate per target class on the same held-out scenes. |

For precision and recall, use an IoU threshold of 0.50 and fix the confidence threshold before evaluation. Record both thresholds with the results.

### Optional extensions

| Metric | Target | How to measure |
| --- | ---: | --- |
| Waypoint patrol success | ≥ 90% (at least 27 of 30 attempts) | Count an attempt as successful if the robot stops within 20 cm of the marked waypoint. Measure distance on the floor independently of the robot's own position estimate. |
| Dashboard alert latency | < 3 s | Measure from local event confirmation to receipt in the dashboard over stable local Wi-Fi. |
