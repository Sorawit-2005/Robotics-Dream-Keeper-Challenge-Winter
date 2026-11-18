# Stage 1 — Ignite | GuardianBot

**Developer:** Sorawit Namwongsa, Kasetsart University Chalermphrakiat Sakon Nakhon Province Campus

**Platform:** D-Robotics RDK X5 with D-Robotics Ubuntu 22.04 and a USB camera

## Challenge 1 — Board Bring-Up

The RDK X5 system image was flashed to a microSD card according to the project notes. The board booted and accepted SSH commands from the development PC over Wi-Fi using Bitvise SSH Client.

- [Booted D-Robotics desktop](Challenge%201%20%E2%80%94%20Board%20Bring-Up/board_bringup.png.png)
- [Active SSH session and terminal output](Challenge%201%20%E2%80%94%20Board%20Bring-Up/challenge1_ssh_connection.png.jpg)

Evidence to add: successful flash screen or log, image build and flashing tool used, and confirmation of internet access from the board.

## Challenge 2 — Sensor Explorer

The USB camera was available through V4L2 at `/dev/video0`. The `cheese` preview showed a graphics driver error. The camera was then previewed through FFmpeg's `ffplay`:

```bash
ffplay -f v4l2 -input_format mjpeg -video_size 640x480 /dev/video0 -loglevel quiet
```

- [Working USB camera image](Challenge%202%20%E2%80%94%20Sensor%20Explorer/sensor_camera_live.jpg.png)
- [Initial camera preview error](Challenge%202%20%E2%80%94%20Sensor%20Explorer/challenge2_camera_error.jpg.png)

## Challenge 3 — First AI Task

The selected on-board AI workload was YOLOv8n object detection. It produced labeled detection boxes from the USB camera.

```bash
yolo predict model=yolov8n.pt source=0 show=True
```

The log identifies the runtime as CPU on aarch64 and reports roughly 1.6 seconds of inference per frame in the visible sample. The 30 FPS entry describes the camera stream.

- [YOLO detection output](Challenge%203%20%E2%80%94%20First%20AI%20Task/yolov8n_detection_result.jpg.png)
- [YOLO command and runtime log](Challenge%203%20%E2%80%94%20First%20AI%20Task/yolov8n_terminal_log.jpg.png)

## When the board is available again

- The original successful flash screen was not captured. Look for a log from the original tool and record the tool and image used. If no log remains, ask the organizers whether the boot and SSH evidence can be accepted as an alternative.
- From the RDK X5 SSH session, run `hostname` and `curl -I --max-time 15 https://github.com`. Capture the terminal response from GitHub with the SSH session visible. Save it with the Challenge 1 evidence.

## Submission checklist

- [x] Collect evidence for active SSH, a working USB camera, and one AI workload.
- [ ] Add successful flash evidence and record proof of internet access.
- [ ] Record the tested installation commands and dependency versions for FFmpeg, Ultralytics, and PyTorch.
- [ ] Verify RDK Studio activation and add the permalink to the Stage 1 check-in in the personal Discord challenge thread.
- [ ] Verify the Showcase PR and review status in the official repository.

[Official Stage 1 requirements](https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge-Winter/blob/main/stages/stage1-ignite.md)
