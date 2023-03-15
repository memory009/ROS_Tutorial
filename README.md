# ROS_Tutorial
## create a catkin workspace

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
```

## carla-ros-bridge
```
# launch carla
cd ~/CARLA_0.9.13/
sh CarlaUE4.sh
# launch carla-ros-bridge
roslaunch carla_ros_bridge carla_ros_bridge_with_example_ego_vehicle.launch
# launch rviz to monitor carla
rviz
```