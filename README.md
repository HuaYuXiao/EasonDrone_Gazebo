# prometheus_gazebo

The prometheus_gazebo package, modified from [prometheus_gazebo](https://github.com/amov-lab/Prometheus/tree/v1.1/Simulator/gazebo_simulator)

![HitCount](https://img.shields.io/endpoint?url=https%3A%2F%2Fhits.dwyl.com%2FHuaYuXiao%2Fprometheus_gazebo.json%3Fcolor%3Dpink)
![Static Badge](https://img.shields.io/badge/ROS-noetic-22314E?logo=ros)
![Static Badge](https://img.shields.io/badge/C%2B%2B-14-00599C?logo=cplusplus)
![Static Badge](https://img.shields.io/badge/Ubuntu-20.04.6-E95420?logo=ubuntu)

![1652374810652053942665216.png](img/1652374810652053942665216.png)


## Release Note

- v1.0.8: 
  - add model `iris`, with Livox LiDAR & D435i RGB-D Camera
  - add model `typhoon_h480`
- v1.0.7: 
  - add `imu` to D435i RGB-D Camera
  - update `frame rate` and `fov` of D435i RGB-D Camera
  - update tf of D435i RGB-D Camera
- v1.0.6: support `launch`
- v1.0.5: import `gazebo_ros_p3d` to get Odometry of camera
- v1.0.4: add `imu` to Velodyne LiDAR
- v1.0.2: add model `P450`, with Velodyne LiDAR & D435i RGB-D Camera


## Compile

```bash
catkin_make install --source Simulator/prometheus_gazebo --build build/prometheus_gazebo
```

```bash
roslaunch prometheus_gazebo GFKD.launch
```
