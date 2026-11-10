# RDK Challenge Winter - Stage 1 (Ignite) 🚀

**Developer:** life (Computer Science, Kasetsart University Chalermphrakiat Sakonnakhon Province Campus)

## 📌 Project Overview
This repository contains the documentation and commands used for Stage 1 of the RDK Challenge Winter using the **RDK X5** board.

## 🛠️ Hardware Setup
* **Board:** RDK X5
* **OS:** Ubuntu 22.04 (D-Robotics)
* **Camera:** USB Camera (`/dev/video0`)

## 📋 Stage 1 Tasks & Execution

### 1. Board Bring-Up
* Flashed OS to microSD card and booted the RDK X5 board.
* Connected via SSH over Wi-Fi (`wlan0` IP: `192.168.1.100`) and USB (`usb0` IP: `192.168.128.10`).
* Command used to SSH:
  ```bash
  ssh sunrise@<IP_ADDRESS>