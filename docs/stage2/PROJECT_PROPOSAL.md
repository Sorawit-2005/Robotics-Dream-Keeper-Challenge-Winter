# Project Proposal: GuardianBot — AI-Powered Smart Home Assistant & Security Robot

- **Project Name:** GuardianBot
- **Category:** Smart Life Robotics
- **Compute Platform:** D-Robotics RDK X5 (Edge AI / BPU)
- **Robot Base:** MasterPi AI Vision Robot Arm with Mecanum Wheels
- **Developer:** Sorawit Namwongsa (Computer Science, Kasetsart University Chalermphrakiat Sakonnakhon Province Campus)

---

## 1. Problem Statement & Concept

Conventional home security systems depend on fixed CCTV cameras that suffer from blind spots, passive recording, and continuous cloud streaming—introducing latency, bandwidth overhead, and household privacy risks. Moreover, homes with elderly residents or unsupervised living zones benefit from an active assistant capable of patrolling rooms and inspecting anomalies on the spot.

**GuardianBot** is an intelligent indoor security and monitoring robot powered by **D-Robotics RDK X5** and built upon the **MasterPi** mobile manipulator platform. The planned robot runs detection on the RDK X5 BPU and decision logic on the CPU. The baseline demo combines person/object detection and tracking with local event capture and supervised low-speed Mecanum movement with a front stop interlock. Waypoint patrol, arm-based inspection and dashboard alerts are extensions.

---

## 2. Operating Scenario & Constraints

- **Operating Environment:** Indoor residential environments (living rooms, hallways, entryways) with flat tiled or wooden floors, household furniture, and mixed natural/artificial indoor lighting.
- **System Constraints:**
  - **Onboard Edge Compute & Power:**
    The RDK X5 serves as the primary onboard computing platform for AI perception, decision-making, and high-level navigation planning.

    Low-level motor and servo control will be handled by the MasterPi controller or a compatible external microcontroller.

    All critical AI processing will operate locally without requiring continuous cloud connectivity.

  - **Privacy-First Design:** Raw video feeds remain strictly on-device; only event-triggered snapshots and status summaries are transmitted to the user dashboard/notification channel.

- **Hardware Safety & Payload Limits:**
  The MasterPi arm with gripper is an optional extension for camera angle adjustment. Confirm the kit revision and joint count before recording the arm specification.

Arm movement and payload limits will be determined through hardware testing before autonomous operation.

- **Incremental Navigation Scope:** The Stage 3 baseline focuses on supervised Mecanum motion and a front range stop. Calibrated waypoint patrol is an extension. Full LiDAR SLAM is future work.

---

## 3. Intended Users & Interaction Model

- **Primary Users:**
  1. **Working Adults & Family Caregivers:** Users away from home who need real-time anomaly alerts, event snapshots, and remote status visibility.
  2. **Elderly Residents & Household Members:** Occupants who need non-intrusive indoor safety monitoring without continuous cloud surveillance.
- **Interaction Model:**
  - **Autonomous Waypoint Patrol (extension):** GuardianBot navigates between predefined checkpoints (e.g., entrance, living room) to inspect surroundings.
  - **Active Multi-Angle Inspection (extension):** Upon detecting an object or region of interest, the robotic arm adjusts the camera
    position and viewing angle to capture a clearer viewpoint.
  - **Event-Driven Recording & Alerts:** When an anomaly rule triggers (e.g., person detected in a restricted zone or path obstruction), the robot halts safely, logs evidence locally, and records a timestamped snapshot. A user dashboard and remote alerts are extensions.

## 4. Hardware Compatibility & Power Architecture

- **Hardware Compatibility:**
  - The RDK X5 will operate as the primary computing platform, while the MasterPi expansion board will provide low-level hardware control where compatible.
  - Communication interfaces, motor drivers, servo controllers, and electrical compatibility must be verified before hardware integration.
  - The MasterPi expansion board is originally designed for Raspberry Pi platforms.
  - Direct compatibility with the RDK X5 has not yet been confirmed.

- Hardware interfaces and control protocols will be inspected before integration.
- If direct compatibility is not possible, a compatible external microcontroller will be used.

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

## 6. Project Scope – MVP กับ Future Development

| Development Priority | Features                                                      |
| :------------------- | :------------------------------------------------------------ |
| **MVP**              | Person/Object Detection and Tracking, Local Event Logging, Supervised Mecanum Movement and Front Range Stop |
| **Advanced**         | Waypoint Patrol, Camera Inspection, Dashboard, Remote Notification               |
| **Future Expansion** | Object Pickup, Advanced Localization, Fall Detection          |

---

## 7. Core Capabilities (Perception – Decision – Actuation)

- **Perception (Sense):**
  - Real-time person detection, object recognition, and object tracking using the Stage 1 USB camera. The MasterPi camera is an alternative after interface verification.

  - Front obstacle detection using the onboard ultrasonic sensor, combined with visual obstacle information where supported.

- **Decision (Think):**
  - The ROS 2 supervisor handles operator commands, the front stop interlock, and event filtering. Waypoint sequencing is added only if the optional patrol is validated.
- **Actuation (Act):**

  - **Omnidirectional Mobility:**
    Four-wheel Mecanum chassis driven by four TT motors for forward, backward, lateral, and rotational movement.

  - **Robotic Manipulation:**
    MasterPi arm with gripper for optional camera adjustment after verifying limits. Object pickup is future work.

  - **Safety Control:**
    Controlled motor stopping and obstacle-aware movement.

  - **Monitoring & Alerting:**
    Local evidence capture, event logging, and status reporting to the dashboard.

---

## 8. Innovation Compared with a Stock Demo

Unlike a standard stationary object-detection demo, GuardianBot combines **Edge AI, omnidirectional mobility, and optional articulated camera inspection** into a unified home robotics system:

1. **Active Camera Re-orientation:** The extension uses the MasterPi arm as an articulated camera positioning mechanism to inspect blind spots and verify anomalies from different viewing angles.
2. **Holonomic Indoor Maneuverability:** Mecanum wheels enable lateral strafing and zero-radius turning around household furniture where differential-drive robots struggle.
3. **Closed-Loop Edge Privacy:** Keeps continuous inference on the RDK X5 BPU while linking visual detections directly to physical motion control and evidence logging.

---

## 9. Measurable Success Targets (KPIs)

These are Stage 3 test targets. Record the actual results and test conditions after running the system.

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
