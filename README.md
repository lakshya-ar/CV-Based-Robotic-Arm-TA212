# Gesture-Controlled 6-DoF Robotic Arm

A Vision-integrated Human-Machine Interface (HMI) that enables real-time, contactless control of a 6-degree-of-freedom robotic manipulator. Developed as part of the **TA212: Manufacturing Processes** course at **IIT Kanpur**, this project replaces traditional hardware controllers with a high-speed Computer Vision pipeline.

## Project Highlights
* **Objective:** Developing a MediaPipe-based system to control 6-DoF robotic arms, evolving from manual hardware interfaces.
* **Core Approach:** * Implemented kinematic mapping and EMA filtering in Python to optimize real-time servo actuation.
  * Integrated MediaPipe frameworks with Arduino and PCA9685 drivers to translate hand landmarks into precise motion.
* **System Impact:** * Established low-latency communication using serial protocols to synchronize software with hardware.
  * Validated robustness across variable lighting, highlighting Computer Vision's viability for contactless manipulation.

## System Architecture & Software Pipeline

### 1. Computer Vision & Mapping (Python)
* **Landmark Detection:** Utilizes MediaPipe to extract 21 3D hand landmarks in real-time.
* **Dynamic Mapping:** Translates pixel-space hand movements (pitch, roll, and depth) into precise angular constraints.
* **Algorithmic Grip Control:** Implements a custom Euclidean distance heuristic between the wrist and fingertips. If the normalized palm ratio falls below a specific threshold, the gripper actuates automatically.

### 2. Signal Processing & Communication
* **EMA Filtering:** To prevent mechanical jitter and stabilize noisy webcam data, an Exponential Moving Average (EMA) filter is applied to the spatial coordinates before transmission.
* **Asynchronous Serial Protocol:** High-speed CSV string packets are sent from the host PC to the Arduino, ensuring minimal latency between physical hand movement and robotic actuation.

### 3. Embedded Firmware (C++)
* **Memory-Efficient Parsing:** The Arduino firmware utilizes `strtok` for fast, lightweight parsing of incoming serial strings.
* **PWM Actuation:** Manages a PCA9685 16-Channel 12-bit PWM driver to accurately position the 6 independently controlled servos.

## Tech Stack
* **Languages:** Python 3, Embedded C++
* **Libraries:** OpenCV, MediaPipe, PySerial, Adafruit PWMServoDriver
* **Hardware Interfaced:** Arduino Uno, PCA9685, 6x Actuators (MG996R & SG90)

## Repository Structure
```text
Gesture-Controlled-Arm/
├── README.md                # Project documentation and setup guide
├── requirements.txt         # Python dependencies
├── hand_tracker.py          # Core CV, spatial mapping, and serial transmission script
├── report.pdf               # Technical report and mechanical design overview
├── servo_control/           
│   └── servo_control.ino    # Embedded C++ firmware for Arduino/PCA9685
└── media/                   # Demonstration videos and system photos
