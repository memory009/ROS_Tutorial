# ROS_Tutorial
* Produced by Qisong He

* reference:http://wiki.ros.org/cn/ROS/Tutorials

# Thanks:
[Chen hengwei](https://gitee.com/chenhengwei)

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

### 文件管理工具的使用
[file management]()

### carla_ros_bridge的使用
[carla_ros_bridge]()

### ROS节点
[rosnode]()

### ROS话题
[rostopic]()
