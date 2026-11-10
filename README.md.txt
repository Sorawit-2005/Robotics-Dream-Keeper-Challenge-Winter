# RDK Challenge Winter - Stage 1 (Ignite) 🚀

**Developer:** life (Computer Science, Kasetsart University Chalermphrakiat Sakonnakhon Province Campus)

## 📌 Project Overview
This repository contains the documentation, logs, and evidence for Stage 1 of the RDK Challenge Winter using the **RDK X5** board.

## 🖥️ Hardware Setup
* **Board:** RDK X5
* **OS:** Ubuntu 22.04 (D-Robotics)
* **Camera:** USB Camera (`/dev/video0`)
---



## 📋 Stage 1 Tasks & Execution

## 🛠️ Challenge Execution Details

### 1. Challenge 1 — Board Bring-Up

* Flashed OS to microSD card and booted the RDK X5 board.
* Connected via SSH over Wi-Fi (`wlan0` IP: `192.168.1.100`)

* **Description:** Successfully flashed the OS image onto the RDK X5 board. Established remote access and management via SSH from the development computer using **PuTTY** and **Bitvise SSH Client**.
* **Evidence:** (Attach your successful SSH connection screenshot)

### 2. Challenge 2 — Sensor Explorer
* **Description:** Connected a USB camera to the RDK X5 board (`/dev/video0`)[cite: 1].
* **Issues Encountered:** Initially, opening the camera preview via the `cheese` application failed despite checking APT packages (due to desktop graphics driver constraints with `vs-drm` on the ARM board).
* **Solution:** Resolved the issue by using `ffplay` to fetch the live video stream directly via the V4L2 interface:
  ```bash
  ffplay -f v4l2 -input_format mjpeg -video_size 640x480 /dev/video0 -loglevel quiet

### 3. Challenge 3 — First AI TaskDescription 
* **Installed the Ultralytics YOLO package on the RDK X5 board and executed real-time object detection.   Command 

* **Used:Bashyolo predict model=yolov8n.pt source=0 show=True

* **Result: The model successfully launched the live preview window, accurately rendering bounding boxes and class labels with a stable performance of around 30 FPS.Evidence: (Attach your YOLO detection preview photo or video clip)