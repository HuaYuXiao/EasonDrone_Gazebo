# Debug record

While running the command below:

```bash
roslaunch uav_simulation uav_simulation.launch
```

![Image](https://github.com/HuaYuXiao/uav_simulation/blob/noetic-devel/Log/2024-03-26/Screenshot%20from%202024-03-26%2017-14-53.png?raw=true)

I get the following error:

```bash
[ERROR] [1711444671.680677946]: Couldn't open joystick /dev/input/js0. Will retry every second.
[ WARN] [1711444672.739160133]: Nothing to publish, octree is empty
[ERROR] [1711444673.091682973]: Waiting for connect PX4!
Warning [parser.cc:833] XML Attribute[version] in element[sdf] not defined in SDF, ignoring.
Warning [parser.cc:833] XML Attribute[version] in element[sdf] not defined in SDF, ignoring.
Warning [parser.cc:833] XML Attribute[version] in element[sdf] not defined in SDF, ignoring.
[ERROR] [1711444677.617069566]: Client [/octomap_server] wants topic /scan to have datatype/md5sum [sensor_msgs/PointCloud2/1158d486dd51d683ce2f1be655c3c181], but our version has [sensor_msgs/LaserScan/90c7ef2dc6895d81024acba2ac42f369]. Dropping connection.
```

![Image](https://github.com/HuaYuXiao/uav_simulation/blob/noetic-devel/Log/2024-03-26/Screenshot%20from%202024-03-26%2017-25-12.png?raw=true)

(**Whole log** can be found here: [roslaunch.log](https://github.com/HuaYuXiao/uav_simulation/blob/noetic-devel/Log/2024-03-26/roslaunch.log)

I search for this error with the command below:

```bash
grep "Waiting for connect PX4!" ~ -r  --binary-files=without-match --exclude-dir=".ros" --exclude-dir=".cache"
```

I get only 1 **useful** result:

```bash
/home/hyx020222/Prometheus/Modules/uav_control/src/uav_control_node.cpp:        ROS_ERROR_STREAM_ONCE("Waiting for connect PX4!");
```

Check `uav_control_node.cpp`, and focus on this part:

```c++
// 检查PX4连接状态
while (ros::ok() && !uav_estimator.uav_state.connected)
{
    // PCOUT(-1, RED, "Waiting for connect PX4!");
    ROS_ERROR_STREAM_ONCE("Waiting for connect PX4!");
    ros::spinOnce();
    //此处需设置4或4以上的值,不然将导致uav_control启动失败的BUG
    ros::Duration(4).sleep();
}
```

Obviously, `ros::ok()` is `true`. Therefore, the problem falls on `uav_estimator.uav_state.connected`.

`uav_estimator` is created in `UAV_estimator uav_estimator(nh);`

**Class** `UAV_estimator` is defined in `uav_estimator.cpp`. 

Search for `uav_state.connected`, I get 3 **useful** results:

1. In line **153**, it is initialized as `false`:

```c++
uav_state.connected = false;
```

2. In line **561**, it is updated by `fake_odom_cb`:

```c++
void UAV_estimator::fake_odom_cb(const nav_msgs::Odometry::ConstPtr &msg)
{
    // uav_state 直接赋值
    uav_state.connected = true;
    uav_state.armed = true;
    uav_state.odom_valid = true;
    uav_state.mode = "OFFBOARD";
    uav_state.position[0] = msg->pose.pose.position.x;
    uav_state.position[1] = msg->pose.pose.position.y;
    uav_state.position[2] = msg->pose.pose.position.z;
    uav_state.velocity[0] = msg->twist.twist.linear.x;
    uav_state.velocity[1] = msg->twist.twist.linear.y;
    uav_state.velocity[2] = msg->twist.twist.linear.z;
    uav_state.attitude_q = msg->pose.pose.orientation;
    Eigen::Quaterniond q = Eigen::Quaterniond(msg->pose.pose.orientation.w, msg->pose.pose.orientation.x, msg->pose.pose.orientation.y, msg->pose.pose.orientation.z);
    Eigen::Vector3d euler = quaternion_to_euler(q);
    uav_state.attitude[0] = euler[0];
    uav_state.attitude[1] = euler[1];
    uav_state.attitude[2] = euler[2];
    uav_state.attitude_rate[0] = 0.0;
    uav_state.attitude_rate[1] = 0.0;
    uav_state.attitude_rate[2] = 0.0;

    uav_state_update = true;
}
```

But actually, I apply `ground_truth` to position for uav, as defined in `uav_control_indoor.yaml`:

```yaml
## parameter for uav_control
control:
    ## 定位源: 0 for MOCAP, 1 for T265, 2 for GAZEBO, 3 for FAKE_ODOM, 4 for GPS, 5 for RTK, 6 for UWB, 7 for VINS, 8 for OpticalFlow
    location_source : 2
```

3. In line **456**, it is updated by `px4_state_cb`:

```c++
void UAV_estimator::px4_state_cb(const mavros_msgs::State::ConstPtr &msg)
{
    uav_state.connected = msg->connected;
    uav_state.armed = msg->armed;
    uav_state.mode = msg->mode;
}
```

`px4_state_cb` is called whenever getting messages from topic `/uav1/mavros/state`.

```c++
// 【订阅】无人机当前状态 - 来自飞控
px4_state_sub = nh.subscribe<mavros_msgs::State>(uav_name + "/mavros/state", 1, &UAV_estimator::px4_state_cb, this);
```

I check `/uav1/mavros/state` with `rostopic echo /uav1/mavros/state`, and get the following output:

```bash
header: 
  seq: 0
  stamp: 
    secs: 1711444170
    nsecs: 135934767
  frame_id: ''
connected: False
armed: False
guided: False
manual_input: False
mode: ''
system_status: 0
---
```

Is it normal that `frame_id` and `mode` are both empty?
