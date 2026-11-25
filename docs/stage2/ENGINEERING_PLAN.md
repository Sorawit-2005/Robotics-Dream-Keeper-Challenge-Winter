# GuardianBot — Engineering Plan

## BOM

Quantities are for one robot. The D-Robotics and Hiwonder links identify the manufacturer or kit. The assembled chassis was inspected from participant photos. Installed describes physical presence. Vendor reference specifications are listed separately from measured or tested values. Verify exact part labels, purchase source if different, and pending electrical details before integration.

| Item | Qty | Supplier / model or kit | Voltage / interface and status |
|---|---:|---|---|
| Compute board | 1 | [D-Robotics RDK X5](https://developer.d-robotics.cc/rdk_doc/en/Quick_start/hardware_introduction/rdk_x5/) | On hand. Dedicated USB-C 5 V / 5 A input per board documentation. |
| Boot storage | 1 | Existing microSD, model to record | Used in Stage 1. Record capacity and OS build. |
| Stage 1 camera | 1 | Existing USB camera, label to record | USB/V4L2 at /dev/video0 tested on RDK X5. Baseline candidate. |
| Arm-mounted camera | 1 | Hiwonder MasterPi kit, exact module to confirm | Installed. A cable is plugged into Pi USB-A and the kit manual specifies USB for its camera. Confirm cable identity and USB enumeration. Keep separate from Stage 1 evidence until confirmed to be the same camera. |
| Chassis, brackets and fasteners | 1 set | [Hiwonder MasterPi kit](https://www.hiwonder.com/products/masterpi) | Mechanical mounting. Confirm fit with RDK and camera. |
| Mecanum wheels and couplings | 4 each | Hiwonder MasterPi kit | Mechanical interface. Confirm wheel orientation. |
| TT gear motors | 4 | Hiwonder MasterPi kit | Motor driver outputs. Verify rated voltage and startup current. |
| Raspberry Pi chassis host | 1 | Raspberry Pi Ltd. — Raspberry Pi 5 Model B (provisional) | Installed below the TurboPi expansion board and planned as the chassis I/O host. Model inferred from the visible port layout. Confirm model and revision on the Pi with `tr -d '\0' </proc/device-tree/model`. RDK X5 remains the AI computer. |
| Expansion/control board | 1 | Hiwonder kit PCB marked TurboPi, exact revision pending | Stacked on the Pi. The layout is consistent with Hiwonder Expansion Board A. Confirm revision, logic levels, motor output ratings and pin mapping before integration. |
| Front ultrasonic sensor | 1 apparent | Hiwonder MasterPi kit, likely Glowy Ultrasonic Sensor | Two cylindrical transducers are visible at the front. Vendor reference for the likely module is 5 V DC, four-pin I2C, address 0x77. Confirm rear label and trace the lead before treating those values as verified on this vehicle. |
| Arm and gripper | 1 assembly | Hiwonder MasterPi kit | Installed. Optional camera angle adjustment. Confirm exact joint count and servo channel mapping. |
| Arm servos | At least 1 per identified model, included in arm assembly | Hiwonder LD-1501MG and LDX-218, labels visible | Manufacturer reference for both models is PWM and 6–8.4 V DC. Count each model and verify the available rail before integration. |
| Battery holder and charger | 1 each | Hiwonder MasterPi kit | Confirm cell chemistry, charger compatibility and wiring. |
| Battery cells | 2 in inventory | Hiwonder MasterPi kit, cell labels to record | Verify cell markings, voltage and current capability. |
| RDK X5 power supply | 1 | Raspberry Pi 27W USB-C Power Supply US, marking P1826 | Label photographed. AC input 100–240 V, 50/60 Hz, 0.8 A. DC outputs 5.1 V / 5.0 A, 9.0 V / 3.0 A, 12.0 V / 2.25 A, or 15.0 V / 1.8 A. RDK X5 packaging recommends USB-C 5 V / 5 A. The participant confirmed this adapter powered the same RDK X5 during Stage 1. Validate operation under the planned Stage 3 workload before the demo. |
| Physical motor stop | 1 planned | Select after verifying actuator rail | Hardware motor drive inhibit or rated power cutoff independent of RDK X5 software. Verify current and accessible mounting. |
| Alternate actuator controller and motor driver | 1 each if required | MCU and rated motor driver, models to be selected only if needed | First evaluate the existing Raspberry Pi and TurboPi-marked board. Use an alternate driver and controller if the existing route fails verification. |
| Regulator and protection | As required | Select after measuring the power budget | Separate actuator power path. Specify regulator, fuse and wiring ratings before assembly. |

## Port inventory

| Board and port group | Photo observation or vendor reference |
| --- | --- |
| Raspberry Pi side ports | USB-C power and two micro-HDMI ports visible. |
| Raspberry Pi end ports | One RJ45 Ethernet and four USB-A ports across two stacks. One USB-A cable is plugged in. Ethernet is a candidate for the RDK X5 link. |
| Pi to expansion board | Expansion PCB is stacked over the Pi GPIO header. Verify the actual revision and bus mapping before designing any alternate host connection. |
| TurboPi-marked board, I2C | A white connector is marked SCL and SDA. Verify the other pin markings, voltage and sensor cable destination on the exact unit. |
| TurboPi-marked board, actuator headers | Three-wire servo plugs and multiple white connectors are visible. Hiwonder's Board A reference documents four motor outputs, six PWM servo ports and two bus-servo ports. Actual connector assignments are pending. |
| TurboPi-marked board, power | A right-angle barrel-style plug and an ON/OFF switch are visible in the upper board area. Exact role, input voltage and polarity are pending. This switch has not been verified as the planned independent motor stop. |

Proposed Stage 3 route: RDK X5 for perception and ROS 2 supervision, with the existing Raspberry Pi and expansion board as the first chassis I/O candidate. Validate the host link, command timeout and safe stopping before using that route for floor tests.

References: [MasterPi kit and camera](https://wiki.hiwonder.com/projects/MasterPi/en/latest/docs/1.getting_ready.html), [Hiwonder Expansion Board A](https://wiki.hiwonder.com/projects/Raspberry-Pi-5-Expansion-Board/en/latest/docs/1_Raspberry_Pi_Expansion_Board_Introduction.html#raspberry-pi-expansion-board-a), [Raspberry Pi ports](https://www.raspberrypi.com/documentation/computers/sbcs.html), [Glowy Ultrasonic Sensor](https://www.hiwonder.com/products/glowing-ultrasonic-sensor), [LD-1501MG](https://wiki.hiwonder.com/projects/ROS-Robot-Control-Board/en/latest/docs/3_RosRobot_Controller_Program_Analysis.html), and [LDX-218](https://www.hiwonder.com/products/ldx-218).

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
