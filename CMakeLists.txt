cmake_minimum_required(VERSION 3.5.1)
project(easondrone_gazebo)

# add_compile_options(-std=c++17)
# set(PYTHON_EXECUTABLE "/usr/bin/python3.8")

find_package(catkin REQUIRED COMPONENTS
  gazebo_dev
  gazebo_msgs
  gazebo_ros    
  # roscpp
)

catkin_package()
