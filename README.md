## Project Description
This repository contains the first laboratory work on robotics. The goal is to design and simulate a mobile robot using the **SDF (Simulation Description Format)** within the **Gazebo Harmonic** environment. The project is fully containerized using **Docker** to ensure environment consistency across different systems.



## Prerequisites
To run this project, you need:
* **Windows 11** with **WSL2** (Ubuntu 24.04)
* **Docker Desktop** (WSL2 backend enabled)
* **WSLg** or an X-server (like VcXsrv) for GUI rendering

---

## Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/IvaGob/robotics_lab2.git
cd robotics_lab2
```
### 2. Build Docker Image

```bash
./scripts/cmd build-docker
```

This takes 10-15 minutes on first run.

### 3. Run Container

```bash
./scripts/cmd run
```
### 4. Install and open VScode

```bash
code .
```


#### Open Additional Terminals for testing

```bash
# In a new terminal window
./scripts/cmd bash
```
---
## Developing
If you created new nodes or made any changes you need to build package again
```bash
# You should already be at /opt/ws when you enter the container

# Build your package
colcon build --packages-select lab2_new

# Source the workspace (makes your package visible)
source install/setup.bash

```
---
## Testing
### Launching
Every time you launch new terminal you need to source the workspace
```bash
source install/setup.bash
```
---
To launch main package use:
```bash
ros2 launch lab2_new gazebo_ros2.launch.py
```
---
### Test the Controller
To start controller publisher you need to start node in the new terminal:
```bash
./scripts/cmd bash
source /opt/ws/install/setup.bash

# Run the robot controller
ros2 run lab2_new robot_controller
```
---
### Test the Subscriber
To test subscriber in yet another terminal launch subscriber node:
```bash
./scripts/cmd bash
source /opt/ws/install/setup.bash

# Run the LiDAR subscriber
ros2 run lab2_new lidar_subscriber
```
Press Ctrl+C to stop  the subscriber node.
### See running nodes and topics
If you want to see what nodes are running now, you can use:
```bash
# See all running nodes
ros2 node list

# Get detailed info about a node
ros2 node info /robot_controller
ros2 node info /lidar_subscriber
```
---
If you want to inspect topics you can use:
```bash
# ROS2 topics
ros2 topic list

# Gazebo topics (for comparison)
gz topic -l

# See who's publishing/subscribing
ros2 topic info /cmd_vel
ros2 topic info /lidar

# See message structure
ros2 interface show geometry_msgs/msg/Twist
ros2 interface show sensor_msgs/msg/LaserScan

# View messages in real-time
ros2 topic echo /cmd_vel
ros2 topic echo /lidar --once
```
