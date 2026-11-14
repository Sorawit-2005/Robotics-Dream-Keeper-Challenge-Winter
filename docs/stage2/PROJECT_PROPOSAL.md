# Project Proposal: GuardianBot — AI-Powered Smart Home Assistant & Security Robot

- **Project Name:** GuardianBot
- **Category:** Smart Life Robotics
- **Compute Platform:** D-Robotics RDK X5 (Edge AI / BPU)
- **Robot Base:** MasterPi AI Vision Robot Arm with Mecanum Wheels
- **Developer:** sorawit (Computer Science, Kasetsart University Chalermphrakiat Sakonnakhon Province Campus)

---

## 1. Problem Statement & Concept

Conventional home security systems depend on fixed CCTV cameras that suffer from blind spots, passive recording, and continuous cloud streaming—introducing latency, bandwidth overhead, and household privacy risks. Moreover, homes with elderly residents or unsupervised living zones benefit from an active assistant capable of patrolling rooms and inspecting anomalies on the spot.

**GuardianBot** is an intelligent indoor security and monitoring robot powered by **D-Robotics RDK X5** and built upon the **MasterPi** mobile manipulator platform. By running computer vision and decision-making locally on the RDK X5 BPU (Edge AI), GuardianBot autonomously patrols designated home waypoints, avoids obstacles using omnidirectional Mecanum wheels, adjusts its camera angle or handles authorized lightweight objects via a 4-DOF robotic arm with gripper, and sends real-time alerts with visual evidence when predefined events occur.

---

## 2. Operating Scenario & Constraints

- **Operating Environment:** Indoor residential environments (living rooms, hallways, entryways) with flat tiled or wooden floors, household furniture, and mixed natural/artificial indoor lighting.
- **System Constraints:**
  - **Onboard Edge Compute & Power:**
    The RDK X5 serves as the primary onboard computing platform for AI perception,decision-making, and high-level navigation planning.

    Low-level motor and servo control will be handled by the MasterPi controller or a compatible external microcontroller.

    All critical AI processing will operate locally without requiring continuous cloud connectivity.

  - **Privacy-First Design:** Raw video feeds remain strictly on-device; only event-triggered snapshots and status summaries are transmitted to the user dashboard/notification channel.

- **Hardware Safety & Payload Limits:**
  The MasterPi 4-DOF robotic arm with gripper will be used for camera angle adjustment and lightweight object manipulation.

Arm movement and payload limits will be determined through hardware testing before autonomous operation.

- **Incremental Navigation Scope:** Stage 2/3 MVP focuses on calibrated waypoint patrol and ultrasonic/vision obstacle avoidance; full LiDAR SLAM is planned as a future expansion.

---

## 3. Intended Users & Interaction Model

- **Primary Users:**
  1. **Working Adults & Family Caregivers:** Users away from home who need real-time anomaly alerts, event snapshots, and remote status visibility.
  2. **Elderly Residents & Household Members:** Occupants who need non-intrusive indoor safety monitoring without continuous cloud surveillance.
- **Interaction Model:**
  - **Autonomous Waypoint Patrol:** GuardianBot navigates between predefined checkpoints (e.g., entrance, living room) to inspect surroundings.
  - **Active Multi-Angle Inspection:** Upon detecting an object or region of interest, the 4-DOF robotic arm adjusts the camera
    position and viewing angle to capture a clearer viewpoint.
  - **Event-Driven Dashboard & Alerts:** When an anomaly rule triggers (e.g., person detected in a restricted zone or path obstruction), the robot halts safely, logs evidence locally, and pushes an alert with timestamped imagery to the user.

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

  The initial navigation system will use a controlled waypoint-based approach.
  The initial navigation system will use calibrated motion commands and available sensor feedback.

Wheel encoder-based odometry will be evaluated as an additional hardware requirement to improve movement estimation and waypoint accuracy.

Until reliable localization is available, waypoint patrol will operate within a controlled and calibrated test environment.
Obstacle detection will use ultrasonic sensing and camera-based perception.
Advanced localization and LiDAR-based SLAM will be considered for future development after the MVP is validated.

## 6. Project Scope – MVP กับ Future Development

| Development Priority | Features                                                      |
| :------------------- | :------------------------------------------------------------ |
| **MVP**              | AI Person Detection, Object Detection, Basic Mecanum Movement |
| **Core Features**    | Obstacle Detection, Event Logging, Camera Inspection          |
| **Advanced**         | Waypoint Patrol, Dashboard, Remote Notification               |
| **Future Expansion** | Object Pickup, Advanced Localization, Fall Detection          |

---

## 7. Core Capabilities (Perception – Decision – Actuation)

- **Perception (Sense):**
  - Real-time person detection, object recognition, and object tracking using the MasterPi camera (480P), subject to verified interface compatibility with the RDK X5.

* Front obstacle detection using the onboard ultrasonic sensor, combined with visual obstacle information where supported.

- **Decision (Think):**
  - ROS 2-based finite state machine managing waypoint patrol sequences, obstacle avoidance behaviors, event filtering, and safety interlocks.
- - **Actuation (Act):**

  - **Omnidirectional Mobility:**
    Four-wheel Mecanum chassis driven by four TT motors for forward, backward, lateral, and rotational movement.

  - **Robotic Manipulation:**
    MasterPi 4-DOF robotic arm with gripper for camera angle adjustment and lightweight object manipulation.

  - **Safety Control:**
    Controlled motor stopping and obstacle-aware movement.

  - **Monitoring & Alerting:**
    Local evidence capture, event logging, and status reporting to the dashboard.

---

## 8. Innovation Compared with a Stock Demo

Unlike a standard stationary object-detection demo, GuardianBot combines **Edge AI, omnidirectional mobility,and articulated camera inspection** into a unified home robotics system:

1. **Active Camera Re-orientation:** Uses the MasterPi 4-DOF robotic arm with gripper as an articulated camera positioning mechanism to inspect blind spots and verify anomalies from different viewing angles.
2. **Holonomic Indoor Maneuverability:** Mecanum wheels enable lateral strafing and zero-radius turning around household furniture where differential-drive robots struggle.
3. **Closed-Loop Edge Privacy:** Keeps continuous inference on the RDK X5 BPU while linking visual detections directly to physical motion control and evidence logging.

---

## 9. Measurable Success Targets (KPIs)

To evaluate system performance in Stage 3, GuardianBot targets the following measurable engineering benchmarks:

| Metric                          | Target              | Evaluation & Measurement Protocol                                                                                                                                                                                     |
| :------------------------------ | :------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **AI Inference Frame Rate**     | $ge 25text{ FPS}$ | Measured end-to-end (including image preprocessing, BPU inference, and post-processing) on RDK X5 running a quantized YOLO model (e.g., YOLOv8n/YOLOv5s `.bin`) at $640 times 480$ resolution.                       |
| **Minimum Obstacle Clearance**  | $ge 20text{ cm}$  | Measured from the closest physical point of the robot chassis to the obstacle after coming to a complete stop, tested at a standard patrol speed of $0.2text{ m/s}$.                                                 |
| **Local Event Logging Latency** | $< 500text{ ms}$   | Elapsed time from the moment an anomaly event is confirmed by the decision node to the completion of local storage write (annotated snapshot + timestamped metadata).                                                 |
| **Dashboard Alert Latency**     | $< 3text{ s}$      | Elapsed time from local event confirmation to alert notification receipt on the user dashboard under stable local Wi-Fi network conditions.                                                                           |
| **Detection Precision**         | $ge 85%$          | Evaluated on an independent, unseen indoor Ground Truth test dataset (separate from training/tuning data), logged separately per target class (`person` and target objects).                                          |
| **Detection Recall**            | $ge 85%$          | Evaluated on the same independent indoor Ground Truth test dataset, logged separately per target class (`person` and target objects).                                                                                 |
| **Waypoint Patrol Completion**  | $ge 90%$          | Achieving at least $27/30$ target waypoints across indoor test runs; a waypoint succeeds when the robot stops within a $pm 20text{ cm}$ position tolerance supported by calibrated odometry/localization reference. |
