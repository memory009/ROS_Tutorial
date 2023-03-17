# ROS_Tutorial
## create a catkin workspace

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
```

## carla-ros-bridge
create a new terminal
```
# launch carla
cd ~/CARLA_0.9.13/
sh CarlaUE4.sh
```

create a new terminal
```
# launch carla-ros-bridge
cd ~/ros_ws/devel/
source setup.bash
cd ..
```

create a new terminal
```
roslaunch carla_ros_bridge carla_ros_bridge_with_example_ego_vehicle.launch
# launch rviz to monitor carla
rviz
```

## 文件管理工具
### 使用rospack
```
rospack find [package_name]
# 将会输出 YOUR_INSTALL_PATH/share/roscpp
```
### 使用roscd



## carla 离屏模式

```
./CarlaUE4.sh -RenderOffScreen
```