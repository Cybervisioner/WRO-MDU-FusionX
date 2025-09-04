# LittleRobot Future Engineers

This repository contains all documentation files for our WRO project. Inside our branches you can find:
- Robot photos
- Team photo
- 3D models
- Source code

---

## 📂 File Description

### 🔹 `main.py`
- Runs on **Pyboard**.
- Waits for a button press to start.
- Receives **speed** and **angle** commands from Raspberry Pi.
- Sends speed directly to the motor.
- Uses a **PID controller** to regulate servo angle.

### 🔹 `qualification.py`
- Runs on **Raspberry Pi** during qualification attempts.
- Captures an image from the camera and extracts 3 regions:
  - Left (for left wall detection)
  - Right (for right wall detection)
  - Bottom (for line counting)
- Converts regions to **HSV color space**.
- Detects walls and centers robot between them using PID control.
- Counts passed lines; after 12 lines, robot stops.

### 🔹 `final.py`
- Similar to `qualification.py`.
- Adds **two extra areas**:
  - One for sign detection (to avoid obstacles).
  - One for direction detection.
- Uses PID control for wall following and navigation.

### 🔹 `RobotAPI.py`
- Library for Raspberry Pi.
- Helps to capture and display camera images while debugging.

### 🔹 `module.py`
- Library for Pyboard.
- Helps to control servo and motor.

---

## 🔧 Connection to Pyboard
1. Connect Pyboard to your computer (appears as a USB flash drive).
2. Copy `main.py` and `module.py` to the board.
3. Wait until the red LED turns off.

✅ Done!

---

## 💻 Connection to Raspberry Pi

### 1. Install Raspberry Pi OS
- Download latest **Raspberry Pi OS (Raspbian)**: [Download here](https://www.raspberrypi.org/software/operating-systems/)
- Flash to microSD card using:
  - **Windows**: Win32 Disk Imager
  - **Mac/Linux**: [Etcher](https://etcher.balena.io)
- Insert SD card, connect HDMI, keyboard, mouse, power → boot system.

📖 Full guide: [How to install Raspbian](https://thepi.io/how-to-install-raspbian-on-the-raspberry-pi/)

### 2. Enable UART
```bash
sudo nano /boot/config.txt
```
At the bottom, add:
```ini
enable_uart=1
```

### 3. Get IP Address
```bash
ifconfig
```
Write down the Ethernet IP address for SSH.

### 4. Autostart robot code
Edit cron jobs:
```bash
crontab -e
```
Add one of the following lines depending on the run:
```bash
@reboot sudo python /home/pi/robot/final.py
# or
@reboot sudo python /home/pi/robot/qualification.py
```

### 5. Enable SSH
```bash
sudo raspi-config
```
- Go to **Interfacing Options → SSH → Enable**

Now you can disconnect HDMI and use only Ethernet + SSH.

### 6. Transfer Files
On Windows, you can use **Bitvise SSH Client**. On Linux/Mac, use:
```bash
scp RobotAPI.py final.py pi@<raspberry_ip>:/home/pi/robot/
```

---

## 🚀 Running the Robot
1. Place robot at the start.
2. Reboot Raspberry Pi.
3. Wait for blue LED on Pyboard.
4. Press the button → Robot starts!

---

## 📸 Media
- Robot photos
- Team photo
- 3D models

(See repository branches/files)

---

👥 **Team:** MDU FusionX

