# GuardianBot — Engineering Plan

## BOM

Quantities are for one robot. The D-Robotics and Hiwonder links identify the manufacturer or kit. Verify exact part labels, purchase source if different, and electrical details marked pending before selection or connection.

| Item | Qty | Supplier / model or kit | Voltage / interface and status |
|---|---:|---|---|
| Compute board | 1 | [D-Robotics RDK X5](https://developer.d-robotics.cc/rdk_doc/en/Quick_start/hardware_introduction/rdk_x5/) | On hand. Dedicated USB-C 5 V / 5 A input per board documentation. |
| Boot storage | 1 | Existing microSD, model to record | Used in Stage 1. Record capacity and OS build. |
| Camera | 1 | Existing Stage 1 USB camera, label to record | USB/V4L2 at /dev/video0 tested. Baseline camera. |
| Chassis, brackets and fasteners | 1 set | [Hiwonder MasterPi kit](https://www.hiwonder.com/products/masterpi) | Mechanical mounting. Confirm fit with RDK and camera. |
| Mecanum wheels and couplings | 4 each | Hiwonder MasterPi kit | Mechanical interface. Confirm wheel orientation. |
| TT gear motors | 4 | Hiwonder MasterPi kit | Motor driver outputs. Verify rated voltage and startup current. |
| Expansion/control board | 1 | Hiwonder MasterPi kit, Raspberry Pi version noted in inventory | Verify revision, control transport, logic levels and motor output ratings. |
| Ultrasonic sensor | 1 planned | Hiwonder MasterPi kit | Confirm presence, revision, interface and supply before use. |
| Arm and gripper | 1 assembly | Hiwonder MasterPi kit | Optional for demo. Verify servo voltage and channel mapping. |
| Battery holder and charger | 1 each | Hiwonder MasterPi kit | Confirm cell chemistry, charger compatibility and wiring. |
| Battery cells | 2 in inventory | Hiwonder MasterPi kit, cell labels to record | Verify cell markings, voltage and current capability. |
| RDK power supply | 1 | D-Robotics RDK X5 compatible supply, select or confirm owned unit | USB-C 5 V / 5 A per board docs. Use separate compute power for bench tests. |
| Physical motor stop | 1 planned | Select after verifying actuator rail | Motor drive inhibit or rated power cutoff. Verify current and accessible mounting. |
| Separate actuator controller and motor driver | 1 each if required | Existing compatible Raspberry Pi if available, or MCU and driver selected after verification | Prefer documented MasterPi control on supported hardware. If unavailable, select rated motor driver and verified host link. |
| Regulator and protection | As required | Select after measuring the power budget | Separate actuator power path. Specify regulator, fuse and wiring ratings before assembly. |

Do not mate the MasterPi header to the RDK X5 based on connector shape. Confirm the board identifiers and compare pinout, voltage, protocol and current limits. First bench-test the motor stop, with the wheels unloaded, using the verified controller. Use separate regulated compute and actuator power in the integration plan.

## Schedule

See the [roadmap through the final demo](../../ROADMAP.md) for dates, dependencies and completion evidence.

## Five main risks

| Risk | Trigger | Mitigation | Fallback |
|---|---|---|---|
| MasterPi control or sensor incompatibility | Datasheet or bench test cannot confirm a supported control link or safe levels | Identify exact revisions and try documented control on supported hardware before integrating. | Use a verified external controller and compatible motor driver/sensor. Keep the robot stationary until controls are verified. |
| Power instability | RDK resets, rail drops out of spec, or protection trips on motor startup | Separate compute from drive power. Measure under startup load, check wiring/protection and validate thermal behavior. | Use a dedicated bench compute supply, reduce actuator scope and retest before floor operation. |
| Unsafe movement | Stale sensor/command, failed watchdog, or minimum measured clearance below 20 cm | Test physical stop and controller watchdog. Start with wheels off the floor and validate clearance at progressively controlled speed. | Disable drive and demonstrate perception with the chassis stationary until the motion gate passes. |
| BPU runtime or throughput issue | Quantized model fails to load, BPU use cannot be demonstrated, or measured throughput is below target | Match sample, image and runtime versions. Capture BPU evidence early and benchmark whole pipeline. | Try a smaller supported model; use CPU only for debug and retain the BPU gate for final submission. |
| Integration exceeds available time | Baseline motion, tracking and event logging fail to run together by the integration checkpoint | Freeze demo scope early and test each subsystem before integration. | Drop arm, dashboard and waypoint extensions. Keep recording dates and report any unfinished gate accurately. |

## Planned GitHub structure

| Path | Contents |
|---|---|
| README.md, ROADMAP.md | Project entry point, stage links and schedule |
| docs/stage2/ | Proposal, architecture, engineering plan and checklist |
| stages/state 1/ | Stage 1 report and evidence |
| src/ | ROS 2 packages for perception, supervisor, hardware bridge and logger |
| launch/ | Bringup and bench-test launch files |
| models/ | Model references, versions, checksums and license notes |
| config/ | Thresholds, rate and hardware settings |
| tests/ | Smoke checks, fault tests and benchmark procedure |
| evidence/stage3/ | Benchmark files, demo links and integration evidence |
