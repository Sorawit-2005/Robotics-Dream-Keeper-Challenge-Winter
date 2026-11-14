# Project Proposal: GuardianBot — AI-Powered Home Security & Monitoring Robot

**Developer:** life (Computer Science, Kasetsart University Chalermphrakiat Sakonnakhon Province Campus)  
**Hardware Platform:** D-Robotics RDK X5  
**Stage:** Stage 2 — Build Challenge (Concept and Application Design)

---

## 1. Concept & Problem Statement
Conventional home security relies heavily on static CCTV cameras that suffer from blind spots, passive recording, and continuous cloud video streaming—raising both privacy concerns and network latency issues. Furthermore, families with elderly members staying home alone need an active, affordable assistant capable of patrolling living spaces and detecting safety anomalies in real time.

**GuardianBot** is an autonomous, AI-powered indoor security and monitoring robot built on the **D-Robotics RDK X5**. By executing computer vision and decision-making locally on the RDK X5 BPU (Edge AI), GuardianBot patrols designated home zones, avoids obstacles, detects people and hazardous events in real time without relying on constant cloud streaming, and immediately alerts users when predefined events occur.

---

## 2. Operating Scenario & Constraints
* **Operating Environment:** Indoor residential spaces (living rooms, hallways, bedrooms) featuring flat tiled or wooden floors, household furniture, and varying indoor lighting conditions (daylight and artificial evening lighting).
* **System Constraints:**
  * **Compute & Power Budget:** All AI inference, navigation, and sensor fusion must run onboard the RDK X5 powered by a mobile battery pack, requiring BPU acceleration to keep CPU load and power draw low.
  * **Privacy Requirement:** Raw continuous video must stay local on the device; only event-triggered snapshots and status logs are transmitted externally.
  * **Connectivity:** Local operation (patrol, obstacle avoidance, audio alarm) must continue functioning even if home Wi-Fi drops temporarily.

---

## 3. Intended Users & Interaction Model
* **Target Users:**
  1. **Working Adults & Family Caregivers:** Individuals who leave home during the day and want real-time visibility into home security and the well-being of elderly relatives.
  2. **Elderly Residents & Home Occupants:** Residents who benefit from non-intrusive indoor safety monitoring and immediate local audio alerts during emergencies.
* **Interaction Model:**
  * **Autonomous Waypoint Patrol:** Users define key checkpoints (e.g., front door, living room, hallway) for scheduled or triggered patrol loops.
  * **Local Audio Feedback:** Upon detecting an anomaly, GuardianBot emits an audible alert or voice warning via an onboard speaker.
  * **Event-Driven Remote Alerts:** When a predefined rule triggers (e.g., unauthorized person detected or potential fall/immobility), the robot captures an annotated snapshot and sends a status notification to the caregiver's messaging channel.

---

## 4. Core Capabilities (Sense – Think – Act)
* **Perception (Sense):**
  * Real-time person and object detection via USB/MIPI camera accelerated on the RDK X5 BPU.
  * Short-range obstacle and boundary detection using distance sensors (LiDAR / Depth / Ultrasonic).
* **Decision (Think):**
  * ROS 2-based state machine managing patrol waypoints, obstacle avoidance maneuvers, and event-filtering logic (e.g., zone intrusion or abnormal posture/inactivity).
* **Actuation (Act):**
  * Differential-drive mobile chassis for smooth indoor navigation.
  * Onboard audio output for immediate local deterrence or alert notifications, paired with asynchronous snapshot reporting.

---

## 5. Innovation Compared with a Stock Demo
Unlike a standard static object-detection demo (such as running `yolo predict` on a stationary webcam), GuardianBot integrates **embodied mobility, edge privacy, and closed-loop event response**:
1. **Active Spatial Coverage:** Replaces static camera blind spots with autonomous multi-waypoint indoor patrol and obstacle avoidance.
2. **Privacy-First Edge Architecture:** Leverages the RDK X5 BPU for local real-time inference, eliminating continuous cloud video uploads while maintaining low-latency response.
3. **Actionable Event Pipeline:** Connects AI perception directly to physical actuation (navigation halt, local audio alarm) and targeted event notifications rather than passive bounding-box visualization.

---

## 6. Measurable Success Targets (KPIs)
To evaluate system performance in Stage 3, GuardianBot targets the following measurable benchmarks:

| Metric | Target Benchmark | Measurement Method |
| :--- | :--- | :--- |
| **AI Inference Speed** | $\ge 25\text{ FPS}$ | Measured on RDK X5 BPU running quantized YOLO model at $640\times 480$ resolution |
| **End-to-End Alert Latency** | $< 500\text{ ms}$ (local alarm) / $< 3\text{ s}$ (remote alert) | Time from event frame capture to audio trigger and notification dispatch |
| **Detection Accuracy** | $\ge 85\%$ Precision / Recall for `person` class | Evaluated across 100 test frames under normal indoor lighting |
| **Navigation & Patrol Success** | $\ge 90\%$ waypoint completion rate | 10 consecutive indoor patrol runs without collision |
| **False Alarm Rate** | $< 10\%$ during normal household activity | Verified using temporal frame confirmation (e.g., event sustained across $\ge 5$ frames) |