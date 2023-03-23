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