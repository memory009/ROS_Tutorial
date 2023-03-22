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
cd ros_ws/devel/
source setup.bash
cd ..
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
```
roscd [locationname[/subdir]]
# 输出工作目录
pwd
```
注意，就像ROS中的其它工具一样，roscd只能切换到那些路径已经包含在ROS_PACKAGE_PATH环境变量中的软件包。要查看 ROS_PACKAGE_PATH中包含的路径，可以输入：
```
echo $ROS_PACKAGE_PATH
```

## carla 离屏模式

```
./CarlaUE4.sh -RenderOffScreen
```

## 为catkin创建一个工作区
```
$ mkdir -p ~/catkin_ws/src
# catkin_ws可以修改为自己的名称加_ws
$ cd ~/catkin_ws/
$ catkin_make
# catkin_make命令在catkin工作空间中是一个非常方便的工具。在你的工作空间中第一次运行它时，它会在src目录下创建一个CMakeLists.txt的链接。
```

使用echo语句查找ros包的的位置
```
echo $ROS_PACKAGE_PATH
# 得到结果/home/daniel/daniel_ws/src:/opt/ros/noetic/share
```

## ROS节点
http://wiki.ros.org/cn/ROS/Tutorials/UnderstandingNodes
* 节点（Nodes）：节点是一个可执行文件，它可以通过ROS来与其他节点进行通信。
* 消息（Messages）：订阅或发布话题时所使用的ROS数据类型。
* 话题（Topics）：节点可以将消息发布到话题，或通过订阅话题来接收消息。
* 主节点（Master）：ROS的命名服务，例如帮助节点发现彼此。
* rosout：在ROS中相当于stdout/stderr（标准输出/标准错误）。
* roscore：主节点 + rosout + 参数服务器（会在以后介绍）。

## 使用roscore
```
# roscore是你在运行所有ROS程序前首先要运行的命令。
roscore
```

## 使用rosnode
```
# 使用rosnode list显示当前正在运行的ros节点信息，如果什么都没看就会显示/rosout，表示只有一个节点在运行：rosout
rosnode list
```

## 使用rosnode info
```
# 使用rosnode info /rosout，返回指定话题（rosout）的节点信息
rosnode info /rosout
```

## 使用rosrun
rosrun可以让你用包名直接运行软件包内的节点（而不需要知道包的路径）,以小乌龟demo为例。
create a new terminal
```
# 格式：rosrun [package_name] [node_name]
rosrun turtlesim turtlesim_node
# 如果想在rosrun之前就设置好节点的名称，可以这样写，这样写的话rosnode list中的名称就会变成自己的名字。
rosrun turtlesim turtlesim_node __name:=my_turtle
```
启动小乌龟demo之后在尝试rosnode list就可以看到小乌龟的节点信息出现在list里面

## 使用ping来看节点是否正常工作
```
# 此处my_turtle需要改为自己的节点名字
rosnode ping my_turtle
```

# building...
（http://wiki.ros.org/cn/ROS/Tutorials）1.1-6理解ros话题