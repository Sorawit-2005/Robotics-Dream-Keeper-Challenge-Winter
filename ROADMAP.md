# GuardianBot Roadmap — RDK Winter 2026

Dates below are project targets. See the [organizer timeline](https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge-Winter/blob/main/TIMELINE.md) for challenge milestones.

| Date | Planned work | Completion evidence |
|---|---|---|
| Nov 19–22 | Review proposal, architecture, BOM and scope. Identify MasterPi revision, sensor and power supply. | Linked documents and list of compatibility decisions or open items. |
| Nov 23–26 | Finalize Stage 2 design and publish the four documents. | Public roadmap, proposal, architecture, engineering plan, Discord permalink and updated Showcase PR. |
| Nov 27–Dec 2 | Validate the official BPU path on RDK X5 and bench-test camera, range and drive interfaces in isolation. | Model/runtime record, BPU-path proof, range logs and unloaded motion/stop evidence. |
| Dec 3–7 | Integrate ROS 2 capture, detection, tracking, event logging and motor control. Test disconnects and stop interlocks. | Reproducible launch, concurrent workloads, local event record, safe stop results. |
| Dec 8–11 | Run repeatable bench and floor tests. Measure accuracy, FPS, event latency and final stopping clearance. | Benchmark table and results with known limitations. |
| Dec 12–15 | Rehearse, record demo and publish final package. | Public video, source and license, quick start and technical docs, benchmarks, final community permalink and Showcase PR. |

Baseline demo: onboard BPU detection with CPU tracking, local event logging and supervised Mecanum motion with front stop protection. Waypoint patrol, camera tilt and dashboard enter the demo only if the baseline is stable and each addition is validated.

Stage 1 follow-up when the board is available is tracked in the [Ignite report](stages/state%201/STAGE1_IGNITE.md).
