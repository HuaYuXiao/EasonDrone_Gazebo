# prometheus_gazebo

The prometheus_gazebo package, modified from [prometheus_gazebo](https://github.com/amov-lab/Prometheus/tree/v1.1/Simulator/gazebo_simulator)

## Release Note

- v1.0.5: Import `gazebo_ros_p3d` to get pose of camera
- **v1.0.4**: Add imu to Velodyne LiDAR
- **v1.0.2**: Create a drone with Velodyne LiDAR & D435i Depth Camera

```bash
catkin_make install --source Simulator/prometheus_gazebo --build build/prometheus_gazebo
```

```bash
roslaunch prometheus_gazebo GFKD.launch
```
