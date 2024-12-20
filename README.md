# EasonDrone_Gazebo

![HitCount](https://img.shields.io/endpoint?url=https%3A%2F%2Fhits.dwyl.com%2FHuaYuXiao%2Feasondrone_gazebo.json%3Fcolor%3Dpink)
![Static Badge](https://img.shields.io/badge/ROS-noetic-22314E?logo=ros)
![Static Badge](https://img.shields.io/badge/C%2B%2B-17-00599C?logo=cplusplus)
![Static Badge](https://img.shields.io/badge/Ubuntu-20.04.6-E95420?logo=ubuntu)

The easondrone_gazebo package.

## Installation

```bash
cd ~/easondrone_ws/simulate
git clone https://github.com/HuaYuXiao/easondrone_gazebo.git
cd ..
rm -rf simulate/easondrone_gazebo/build
catkin_make --source simulate/easondrone_gazebo --build simulate/easondrone_gazebo/build
```

## Launch

```bash
roslaunch easondrone_gazebo simulation.launch
```

## Acknowledgement

Thanks for following packages:

- [prometheus_gazebo](https://github.com/amov-lab/Prometheus/Simulator/gazebo_simulator)
- [livox_laser_simulation](https://github.com/Livox-SDK/livox_laser_simulation)
