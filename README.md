# EasonDrone_Gazebo

The easondrone_gazebo package.

![HitCount](https://img.shields.io/endpoint?url=https%3A%2F%2Fhits.dwyl.com%2FHuaYuXiao%2Feasondrone_gazebo.json%3Fcolor%3Dpink)
![Static Badge](https://img.shields.io/badge/ROS-noetic-22314E?logo=ros)
![Static Badge](https://img.shields.io/badge/C%2B%2B-14-00599C?logo=cplusplus)
![Static Badge](https://img.shields.io/badge/Ubuntu-20.04.6-E95420?logo=ubuntu)

![1652374810652053942665216.png](img/1652374810652053942665216.png)


## Compilation

```shell
cd ~/EasonDrone
catkin_make install --source Simulator/EasonDrone_Gazebo --build Simulator/EasonDrone_Gazebo/build
```


## Launch

For p450:

```shell
roslaunch easondrone_gazebo simu_p450.launch
```

For iris:

```shell
roslaunch easondrone_gazebo simu_iris.launch
```


## Acknowledgement

Thanks to following packages:

- [prometheus_gazebo](https://github.com/amov-lab/Prometheus/Simulator/gazebo_simulator)
- [sitl_gazebo](https://github.com/PX4/sitl_gazebo)
