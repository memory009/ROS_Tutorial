# ROS_Tutorial
* Produced by Qisong He

* reference:http://wiki.ros.org/cn/ROS/Tutorials

# Thanks:
[Chen hengwei](https://gitee.com/chenhengwei)

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
#######################################################################

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

#######################################################################
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


## 小乌龟demo
```
roscore
```

create a new terminal
```
rosrun turtlesim turtlesim_node
```

create a new terminal
```
#ultilize keyboard to operate turtle's position
rosrun turtlesim turtle_teleop_key
```

create a new terminal
```
#rqt_graph用动态的图显示了系统中正在发生的事情
rosrun rqt_graph rqt_graph
```

报错```‘PluginHandlerDirect._restore_settings() plugin "rqt_graph/RosGraph#0" raised an exception:```

执行命令：
```sudo dot -c```

https://blog.csdn.net/qq_49756908/article/details/126669694


# 学习rostopic
## 使用rostopic echo 显示在某个话题上发布的数据
```
# 用法
rostopic echo [topic]
# 例子
rostopic list #查看目前有哪些话题
rostopic echo /turtle1/cmd_vel #以/turtle1/cmd_vel话题为例，查看话题上发布的数据
###########################################################################
---
linear: 
  x: 2.0
  y: 0.0
  z: 0.0
angular: 
  x: 0.0
  y: 0.0
  z: 0.0
###########################################################################
```

## 使用rostopic list列出当前已被订阅和发布的所有话题
```
rostopic list
```

## 使用rostopic type命令用来查看所发布话题的消息类型
```
rostopic type [topic]
```
e.g. run 'rostopic type /turtle1/cmd_vel'in terminal
output : geometry_msgs/Twist

## 使用rosmsg查看消息的详细信息：
```
# e.g.
rosmsg show geometry_msgs/Twist
# output:
geometry_msgs/Vector3 linear
  float64 x
  float64 y
  float64 z
geometry_msgs/Vector3 angular
  float64 x
  float64 y
  float64 z
```

## 使用rostopic pub 把数据发布到当前某个正在广播的话题上
```
# e.g.
# rostopic pub [topic] [msg_type] [args]
rostopic pub -1 /turtle1/cmd_vel geometry_msgs/Twist -- '[2.0, 0.0, 0.0]' '[0.0, 0.0, 1.8]'
# 以上命令会发送一条消息给turtlesim，告诉它以2.0大小的线速度和1.8大小的角速度移动
```
解析：
* 这条命令将消息发布到指定的话题：
```
rostopic pub
```
* 这一选项会让rostopic只发布一条消息，然后退出：
```
-1 
```
* 这是要发布到的话题的名称：
```
/turtle1/cmd_vel
```
* 这是发布到话题时要使用的消息的类型：
```
geometry_msgs/Twist
```
* 这一选项（两个破折号）用来告诉选项解析器，表明之后的参数都不是选项。如果参数前有破折号（-）比如负数，那么这是必需的
```
--
```
* 一个turtlesim/Velocity消息有两个浮点型元素：linear和angular。在本例中，'[2.0, 0.0, 0.0]'表示linear的值为x=2.0, y=0.0, z=0.0，而'[0.0, 0.0, 1.8]'是说angular的值为x=0.0, y=0.0, z=1.8。这些参数实际上使用的是YAML语法，在YAML命令行文档中有描述。
YAML命令行文档:http://wiki.ros.org/ROS/YAMLCommandLine
```
'[2.0, 0.0, 0.0]' '[0.0, 0.0, 1.8]' 
```

## 使用rostopic hz 报告数据发布的速率
```
# 用法 
rostopic hz [topic]
# e.g. 
rostopic hz /turtle1/pose
```
output：
```
subscribed to [/turtle1/pose]
average rate: 59.354
        min: 0.005s max: 0.027s std dev: 0.00284s window: 58
average rate: 59.459
        min: 0.005s max: 0.027s std dev: 0.00271s window: 118
average rate: 59.539
        min: 0.004s max: 0.030s std dev: 0.00339s window: 177
average rate: 59.492
        min: 0.004s max: 0.030s std dev: 0.00380s window: 237
average rate: 59.463
        min: 0.004s max: 0.030s std dev: 0.00380s window: 290

```
