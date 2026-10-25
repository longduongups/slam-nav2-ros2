# ROS 2 Autonomous Navigation, SLAM + Nav2

Autonomous navigation stack built on ROS 2 Humble. Mapping with SLAM Toolbox and autonomous frontier exploration, navigation on saved map with Nav2, and benchmark of 3 Nav2 controllers (DWB, MPPI, RPP). Sensor fusion odometry + IMU via robot_localization EKF.

## Features

- Mapping with SLAM Toolbox, loop closures
- Autonomous frontier exploration
- Navigation on saved map (AMCL localization)
- Benchmark of Nav2 controllers DWB vs MPPI vs RPP
- Odometry + IMU fusion via robot_localization EKF
- Simulation Gazebo + real robot ready

## Stack

```
ROS 2 Humble
SLAM Toolbox
Nav2 (navigation2)
robot_localization (EKF)
Gazebo Classic
RViz 2
```

## Repository structure

```
.
├── src/
│   ├── rosnav_bot/
│   │   ├── launch/
│   │   ├── config/
│   │   │   ├── nav2_params.yaml
│   │   │   ├── slam_params.yaml
│   │   │   └── ekf.yaml
│   │   ├── maps/
│   │   ├── urdf/
│   │   ├── rviz/
│   │   ├── CMakeLists.txt
│   │   └── package.xml
├── docs/
│   └── slam_demo.gif
├── .gitignore
├── LICENSE
└── README.md
```

## Prerequisites

Ubuntu 22.04 + ROS 2 Humble installed.

```bash
sudo apt install -y \
    ros-humble-slam-toolbox \
    ros-humble-navigation2 \
    ros-humble-nav2-bringup \
    ros-humble-robot-localization \
    ros-humble-turtlebot3* \
    ros-humble-gazebo-ros-pkgs
```

## Build

```bash
git clone https://github.com/longduongups/ros2-slam-navigation.git
cd ros2-slam-navigation
colcon build --symlink-install
source install/setup.bash
```

## Usage

### 1. Launch simulation Gazebo

```bash
ros2 launch rosnav_bot gazebo_sim.launch.py
```

### 2. Mapping (SLAM)

```bash
ros2 launch <nom_du_package> slam.launch.py
# Drive the robot with teleop
ros2 run teleop_twist_keyboard teleop_twist_keyboard
# Save the map
ros2 run nav2_map_server map_saver_cli -f src/<nom_du_package>/maps/my_map
```

### 3. Navigation on saved map

```bash
ros2 launch rosnav_bot navigation.launch.py \
    map:=src/rosnav_bot/maps/my_map.yaml
```

### 4. Switch Nav2 controller

Edit `config/nav2_params.yaml`, section `controller_server`, `FollowPath.plugin`.

```
dwb_core::DWBLocalPlanner        # DWB (default)
nav2_mppi_controller::MPPIController   # MPPI
nav2_regulated_pure_pursuit_controller::RegulatedPurePursuitController   # RPP
```

## Benchmark results

| Controller | Path tracking error | Avg speed | Collisions |
|------------|---------------------|-----------|------------|
| DWB        | TODO                | TODO      | TODO       |
| MPPI       | TODO                | TODO      | TODO       |
| RPP        | TODO                | TODO      | TODO       |



