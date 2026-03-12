# Autonomous Navigation Stack (ROS2 + SLAM)

Autonomous navigation system developed for the **Advanced Robotics (MCEN 5302)** course at the **University of Colorado Boulder**.

This project implements a **hybrid perception and navigation pipeline** that enables an **AWS DeepRacer robot** to autonomously navigate a closed indoor track using a combination of:

- LiDAR-based SLAM
- Vision-based tape detection
- Global path planning
- ROS2 navigation stack

The system was designed for a **robotics competition requiring autonomous completion of multiple laps around a predefined track with minimal human intervention.**

## Team Repository
The original implementation repository is hosted here:

https://github.com/jnealo32/tne-robotics

---

# Project Overview

The objective of this project was to design a **fully autonomous navigation controller** capable of completing **multiple laps of an indoor course** while maintaining:

- high navigation reliability
- consistent lap times
- minimal collisions or human intervention

To achieve this, we developed a **dual-mode navigation architecture** combining:

1. **Vision-based tape following**  
2. **LiDAR-based SLAM and global path planning**

This hybrid approach allowed the system to maintain **robust navigation even when individual sensing modalities became unreliable**.

---

# System Architecture

The navigation system was built on the **AWS DeepRacer robotic platform** and implemented using **ROS2 Humble**.

### Hardware Platform

**Compute**
- Raspberry Pi 4 Model B (4GB RAM)
- Ubuntu 22.04
- ROS2 Humble

**Sensors**

**LiDAR**
- RP LiDAR A1
- 360° scanning
- 0.15m – 12m range
- ~1° angular resolution

**Camera**
- Intel RealSense D435i
- 640×480 resolution
- RGB stream used for vision-based detection

**Control Hardware**
- Pixhawk 4 Mini flight controller
- ArduPilot Rover firmware
- MAVLink communication

---

# Software Stack

- **ROS2 Humble**
- **slam_toolbox** for SLAM mapping
- **NAV2** for path planning and navigation
- **OpenCV** for tape detection
- **MAVLink** communication with vehicle controller

---

# Navigation Pipeline

The system follows a modular ROS2 architecture consisting of several interacting nodes.

### 1. Perception Layer

**Tape Detection Node**
- Uses OpenCV to detect track boundary tape
- Extracts lane position information from camera frames
- Outputs steering commands for reactive navigation

---

### 2. Mapping and Localization

**SLAM Node**
- Implemented using `slam_toolbox`
- Generates an occupancy grid map of the environment using LiDAR data
- Enables global localization of the vehicle

---

### 3. Path Planning

Using the **NAV2 navigation stack**:

- Waypoints are defined on the generated occupancy map
- Global paths are computed between waypoints
- The robot follows planned trajectories around the course

---

### 4. Control Layer

The controller node:

- converts navigation outputs into velocity commands
- publishes **linear and angular velocity commands**
- communicates with the Pixhawk controller via MAVLink

---

# Hybrid Navigation Strategy

The final system used a **dual-mode navigation strategy**:

### Vision Mode
Used for:
- tape following
- lane tracking
- quick reactive navigation

### SLAM + Global Navigation Mode
Used for:
- localization
- mapping
- waypoint navigation
- trajectory planning

This hybrid design improved **robustness and repeatability** during the competition.

---

# System Diagram

*(Add architecture diagram here if available)*
