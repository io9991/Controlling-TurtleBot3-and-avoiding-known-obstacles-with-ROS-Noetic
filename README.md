# 🐢 TurtleBot3 Autonomous Navigation & Obstacle Avoidance

![ROS](https://img.shields.io/badge/ROS-Noetic-22314E?style=for-the-badge&logo=ros&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![MATLAB](https://img.shields.io/badge/MATLAB-e16737?style=for-the-badge&logo=mathworks&logoColor=white)

A comprehensive robotics project focused on the kinematic control, local path planning, and known-obstacle avoidance of a differential drive mobile robot[cite: 3]. Developed as a Computer Engineering Degree Thesis at Università della Calabria[cite: 3].

This repository contains the simulation environments, ROS launch files, and MATLAB data analysis scripts used to evaluate the performance of the **Dynamic Window Approach (DWA)** within the ROS Navigation Stack[cite: 3].

<p align="center">
  <img src="link_alla_tua_gif_di_rviz_o_gazebo.gif" width="600" alt="TurtleBot3 navigating in RViz/Gazebo">
</p>
*The TurtleBot3 Waffle autonomously navigating a maze avoiding known obstacles using DWA and AMCL[cite: 3].*

## 🚀 Engineering Highlights

* **Differential Kinematic Control:** Implemented theoretical models for direct and inverse kinematics specific to differential drive constraints (non-holonomic constraints)[cite: 3].
* **Feedback Control Law:** Designed a multivariable proportional controller based on an error model (linearized around the operating point) to accurately track pre-calculated trajectories[cite: 3].
* **Dynamic Window Approach (DWA):** Utilized the DWA local planner to operate directly in the velocity space (linear and angular velocities)[cite: 3]. The algorithm evaluates safe trajectories based on target heading, obstacle clearance, and speed maximization while respecting the robot's physical acceleration limits[cite: 3].
* **ROS Navigation Stack Integration:** Full configuration of the `move_base` node, integrating global/local costmaps, `global_planner`, and recovery behaviors (e.g., `rotate_recovery`)[cite: 3].
* **Probabilistic Localization:** Employed Adaptive Monte Carlo Localization (AMCL) combined with a particle filter to accurately track the robot's pose within pre-mapped environments[cite: 3].

## 🛠️ Hardware & Software Setup

### Hardware
* **Robot:** TurtleBot3 Waffle[cite: 3].
* **Computing:** Raspberry Pi 4 (SBC) and 32-bit ARM Cortex-M7 OpenCR1.0 (MCU)[cite: 3].
* **Sensors:** LDS-01 / LDS-02 2D Laser Scanner (Lidar) for environmental mapping and obstacle detection[cite: 3].

### Software Ecosystem
* **Framework:** ROS Noetic[cite: 3].
* **Simulation:** Gazebo (3D physics) and RViz (real-time telemetry and map visualization)[cite: 3].
* **Data Processing:** `rosbag` for logging telemetry data (topics like `/cmd_vel`, `/odom`, `/amcl_pose`)[cite: 3].
* **Analysis:** MATLAB scripts used to extract bag data and plot trajectory tracking, linear/angular velocities, and goal distance metrics[cite: 3].

## 📊 Evaluation & Scenarios

The control architecture was rigorously tested under varying degrees of spatial complexity[cite: 3].

### 1. Virtual Simulations (Gazebo & RViz)
Created custom 3D maze environments via Gazebo's Building Editor and mapped them using the `turtlebot3_slam` node[cite: 3]. The DWA algorithm was tested across **5 different scenarios** with incrementally placed obstacles to evaluate path recalculation and edge-case failures (e.g., tight corners causing the robot to abort the goal)[cite: 3].

### 2. Real-World Physical Testing
Transitioned the simulated parameters to the physical TurtleBot3 in a laboratory environment[cite: 3]. Conducted **4 physical scenarios** comparing real-world odometry drifts and Lidar noise against the simulated baseline[cite: 3]. 

<p align="center">
  <img src="link_foto_laboratorio.jpg" width="45%" alt="Real world lab setup" />
  <img src="link_grafico_matlab.png" width="45%" alt="MATLAB telemetry data" />
</p>
*Left: Physical laboratory obstacle course[cite: 3]. Right: MATLAB evaluation of angular velocity and trajectory tracking extracted from rosbag data[cite: 3].*

## 💻 Repository Structure
* `/launch/`: Custom `.launch` files (`start_localization.launch`, `start_navigation.launch`) tying together maps, AMCL, and `move_base`[cite: 3].
* `/param/`: YAML configuration files tuning the DWA parameters, global/local costmaps, and kinematic limits[cite: 3].
* `/maps/`: `.yaml` and `.pgm` files representing the 2D occupancy grids generated via SLAM (gmapping)[cite: 3].
* `/matlab_analysis/`: Scripts to parse `.bag` files and generate performance metrics (total time, distance traveled, minimum goal distance)[cite: 3].
