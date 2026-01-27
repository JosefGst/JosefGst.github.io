---
draft: false
date: 2025-09-09
categories:
  - Robotics
  - Hong Kong Center for Construction Robotics | HKCRC

---


# :sweat_drops: Water Tank Cleaning Robot | HKCRC

![full_demo_real_robot](assets/full_demo_real_robot.gif)

## 🛠️ Technology Stack
- [ROS2](https://docs.ros.org/en/jazzy/index.html)
- C++, Python, Docker
- [SLAM, Nav2](https://docs.nav2.org/index.html)
- [Gazebo Simulation](https://gazebosim.org/docs/all/getstarted/)
- [Behavior_tree_cpp](https://www.behaviortree.dev/)

<!-- more -->


## ❓ Problem Statement

Potable water tanks require regular cleaning to ensure water quality and safety. Traditional cleaning methods are labor-intensive, time-consuming, and pose health risks to workers due to exposure to contaminants.
![manual_cleaning](assets/manual_cleaning.jpg)
<!-- ![emsd_water_tank](assets/emsd_water_tank.jpg) -->

## 💡 Proposed Solution
To address this, we are developing an autonomous cleaning robot using a high-pressure water jet mounted on the robot to clean the tank surfaces effectively. The robot first follows the wall and cleans the wall surfaces while mapping the environment. After that, it performs coverage path planning to ensure all areas of the floor and ceiling are cleaned as well.

>TODO: Add real cleaning demo here video once available. What to see: real robot operating inside water tank, cleaning wall, floor, ceiling.

## 🤖 My Contributions
  1. 🗺️ When I started, the robot was an uncontrollable mess. The minimum velocity was too high, the PID not tuned. Mechanically and control software still under construction but after setting up a simple Gazebo simulation I was back on track and full speed in development.
  2. 🧹 I dove into ROS2’s navigation stack, wrestling with SLAM until the robot could finally map its surroundings. Further added opennav_coverage. All of this works very well together since they are the most popular stack for these tasks and the setup was straightforward.
    ![demo](assets/demo.gif)
  3. 🌳 To continue, I created a wall-following task using behavior trees, which serves two purposes. First, the robot uses the water jet to clean the wall. Secondly, at the same time, it maps the environment. [Behavior_tree_cpp](https://www.behaviortree.dev/) is the most popular library for this and is also used internally in [Nav2](https://docs.nav2.org/index.html). Tasks can be split up into their smallest entities and later combined together to fulfill complex tasks and recover from failures.
    ![bt](assets/bt.png)
  4. 🐳 The first version of the robot used the Raspberry Pi 5. For the second version, it was upgraded to the Jetson Orin Nano because the computer vision needed higher performance. Thanks to that upgrade, suddenly the whole ROS workspace could not be installed anymore because on the Pi the Ubuntu version was 24.04, but on Jetson you have to install Jetpack which is equivalent to Ubuntu 22.04. Docker saved the day and helped me to dodge the dependency hell by creating a modular Docker environment. It streamlined the development process for both simulation and real robot deployment, utilizing a development container which can attach to any other container. It includes all dev-tools and keeps the deployable image small and clean.
    ![docker_container_structure](assets/docker_container_structure.png)
  5. After everything worked fine it was time for challenging the robot. Testing very narrow environments and very large ones or adding unmapped obstacles. The coverage planner seemed promising, but it failed spectacularly with obstacle avoidance. The open nav2 coverage planner is based on fields2cover and it works very well to create paths which cover the whole area. Although you can define obstacles in the map, the planner will [Not considering holes when path planning #50](https://github.com/open-navigation/opennav_coverage/issues/50). Dynamic obstacle avoidance is also not working look at Issue 👉 [Skip waypoints if occupied #68](https://github.com/open-navigation/opennav_coverage/issues/68). This was a herb set back, since I though this should work out of the box naturally.
  6. 🤯 I was surprised when obstacle avoidance didn’t work out of the box. After some head-scratching and research, we had to build our own planner. It takes the map image and uses computer vision to create goal poses in a swath pattern style which can be used by the DWB planner. By following the goal poses, the robot's global planner can replan when the robot gets stuck and the local planner will avoid unmapped obstacles. It is not perfect yet. When avoiding obstacles some areas won't be covered. But it's a progress.
    ![waypoint_demo](assets/waypoint_demo.gif)


## 🏆 Lessons Learned

  - 🌳 Behavior trees enable fast orchestration and easy modification of all the smallest behavior actions. But for non-blocking, long-lasting tasks, ROS action servers are the way to go. The behavior-task will act only as a remote switch to control the action server. That way it won't block the tree.
  - 🧹 Open nav2 based on fields2cover is reliable and works out of the box with nav2. Although it is possible to define additional polygons inside the main field as obstacles, paths are still planned through the obstacle area.
  - 🤯 Obstacle avoidance is not supported in open nav2 coverage planner.
  - 🐳 The modular Docker environment accelerated development and ensures all dependencies are up to date when deploying to a new environment.

  ## 🏆 Lessons Learned

Building this robot was a crash course in both robotics and humility. I quickly learned that even the most popular tools—like ROS2’s navigation stack and coverage planners—don’t always work as expected. Wrestling with Docker to tame dependency chaos was frustrating at first, but ultimately empowering; it turned what could have been weeks of setup headaches into a streamlined workflow. The biggest surprise was how much behavior trees simplified complex task orchestration, letting me recover from failures and tweak behaviors on the fly. Every setback, from hardware upgrades to planner limitations, forced me to dig deeper and get creative. In the end, the project taught me new tools which I will reuse in future robot building endeavors.
