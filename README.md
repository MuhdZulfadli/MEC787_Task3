# Task 3: ROS2 SLAM with TurtleBot3

## Objectives
- Understand SLAM (Simultaneous Localization and Mapping) in theory and practice.
- Build a map using TurtleBot3 simulation (Gazebo).
- Replicate the same process on a real TurtleBot3 robot.
- Save map files for navigation.
- Compare results between simulation and real robot.

---

## Requirements
- Ubuntu 22.04 + ROS2 Humble + TurtleBot3 packages + Gazebo + RViz2  
- TurtleBot3 Burger/Waffle (with LIDAR, OpenCR, Raspberry Pi)  
- Wi-Fi connection between robot and laptop  
- slam_toolbox or cartographer installed  

---

## A) Simulation (Gazebo)

1. Launch world  
   ```bash
   export TURTLEBOT3_MODEL=burger
   ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py

2. Run SLAM
   - Cartographer
     ```bash
     ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
   - Toolbox (Humble)
     ```bash
     ros2 launch slam_toolbox online_async_launch.py use_sim_time:=True

3. Teleoperate robot
   ```bash
   ros2 run turtlebot3_teleop teleop_keyboard

   # Drive until the enviroment is fully mapped

4. Save map
   ```bash
   ros2 run nav2_map_server map_saver_cli -f ~/sim_map

---

## B) Real Robot (Lab Environment)

1. Connect laptop and TurtleBot3 to the same Wi-Fi.

2. Set environment variables (on laptop):
   ```bash
   export ROS_DOMAIN_ID=30   # must match robot
   export TURTLEBOT3_MODEL=burger

3. SSH into robot (Raspberry Pi):
   ```bash
   ssh ubuntu@<robot_ip>

4. On robot: bringup drivers
   ```bash
   ros2 launch turtlebot3_bringup robot.launch.py

5. On laptop: run SLAM
   - Cartographer
     ```bash
     ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
   - Toolbox (Humble)
     ```bash
     ros2 launch slam_toolbox online_async_launch.py use_sim_time:=True

6. Teleoperate robot (from laptop)
   ```bash
   ros2 run turtlebot3_teleop teleop_keyboard

   # Drive until the enviroment is fully mapped

7. Save map (on laptop)
   ```bash
   ros2 run nav2_map_server map_saver_cli -f ~/sim_map
