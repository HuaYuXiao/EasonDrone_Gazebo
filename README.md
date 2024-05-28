# EasonDrone_Gazebo

The easondrone_gazebo package.

![HitCount](https://img.shields.io/endpoint?url=https%3A%2F%2Fhits.dwyl.com%2FHuaYuXiao%2Feasondrone_gazebo.json%3Fcolor%3Dpink)
![Static Badge](https://img.shields.io/badge/ROS-noetic-22314E?logo=ros)
![Static Badge](https://img.shields.io/badge/C%2B%2B-14-00599C?logo=cplusplus)
![Static Badge](https://img.shields.io/badge/Ubuntu-20.04.6-E95420?logo=ubuntu)

![1652374810652053942665216.png](img/1652374810652053942665216.png)


## Drone Model

### iris

- 2D LiDAR
- 3D LiDAR
- D435i

### P450

- 2D LiDAR
- 3D LiDAR
- D435i

### typhoon_h480


## Compilation

```bash
catkin_make install --source Simulator/easondrone_gazebo --build build/easondrone_gazebo
```


## Launch

PX4 official:

```bash
roslaunch px4 mavros_posix_sitl.launch
```

For iris:

```bash
roslaunch prometheus_gazebo simu_iris.launch
python3 ~/Prometheus/Modules/uav_control/script/multirotor_communication.py iris 0
python3 ~/Prometheus/Modules/uav_control/script/multirotor_keyboard_control.py iris 1 vel
```

For p450:

```bash
roslaunch prometheus_gazebo simu_p450.launch
```


## Release Note

- v1.1.0:
  - add model `iris`, with Livox LiDAR & D435i RGB-D Camera
  - add model `typhoon_h480`
- v1.0.8:
  - add world `base`
  - add world `cic2021`
  - update tf of `P450`
- v1.0.7:
  - add `imu` to D435i RGB-D Camera
  - update `frame rate` and `fov` of D435i RGB-D Camera
  - update tf of D435i RGB-D Camera
- v1.0.6: support `launch`
- v1.0.5: import `gazebo_ros_p3d` to get Odometry of camera
- v1.0.4: add `imu` to Velodyne LiDAR
- v1.0.2: add model `P450`, with Velodyne LiDAR & D435i RGB-D Camera


## Acknowledgement

Thanks to following packages:

- [prometheus_gazebo](https://github.com/amov-lab/Prometheus/tree/v1.1/Simulator/gazebo_simulator)
- 