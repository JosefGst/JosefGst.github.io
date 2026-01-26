---
draft: false
date: 2025-09-09
categories:
  - Robotics
---


# :sweat_drops: Water Tank Cleaning Robot

![full_demo_real_robot](assets/full_demo_real_robot.gif)

## 🛠️ Technology Stack
- ROS2
- C++, Python, Docker
- SLAM, Navigation2
- Gazebo Simulation
- Behavior Trees

<!-- more -->

## 🤖 My Contributions
  - 🗺️ Setting up SLAM, navigation, and coverage path planning for an autonomous water tank cleaning robot using ROS2 and the Gazebo simulation environment.
    ![demo](assets/demo.gif)
  - 🌳 Using Behavior Trees for reliable task execution and recovery behaviors to handle unexpected situations.
    ![bt](assets/bt.png)
  - 🐳 Developed a modular Docker-based development environment to streamline the development and testing process for both simulation and real robot deployment.
    ![docker_container_structure](assets/docker_container_structure.png)

## ❓ Problem Statement

Potable water tanks require regular cleaning to ensure water quality and safety. Traditional cleaning methods are labor-intensive, time-consuming, and pose health risks to workers due to exposure to contaminants.
![emsd_water_tank](assets/emsd_water_tank.jpg)

## 💡 Solution
To address these, we developed an autonomous cleaning robot using a high-pressure water jet mounted on the robot to clean the tank surfaces effectively. The robot first follows the wall and cleans the wall surfaces while mapping the environment. After that, it performs coverage path planning to ensure all areas of the floor and ceiling are cleaned as well.

TODO: Add real cleaning demo here video once available.

## 🏆 Results & Impact

  - 🤖 Successfully demonstrated autonomous cleaning real-world water-tank environments.
  - 🧹 Achieved full coverage of tank surfaces with reliable navigation and obstacle avoidance.
  - 👷‍♂️ Reduced manual labor and improved safety by minimizing human entry into confined spaces.
  - ⚡ The modular Docker environment accelerated development and ensures all dependencies are up to date.
