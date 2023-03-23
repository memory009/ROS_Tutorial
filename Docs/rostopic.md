## 使用rostopic echo 显示在某个话题上发布的数据
```
# 用法
$ rostopic echo [topic]
# 例子
$ rostopic list #查看目前有哪些话题
$ rostopic echo /turtle1/cmd_vel #以/turtle1/cmd_vel话题为例，查看话题上发布的数据
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
$ rostopic list
```

## 使用rostopic type命令用来查看所发布话题的消息类型
```
$ rostopic type [topic]
```
e.g. run 'rostopic type /turtle1/cmd_vel'in terminal
output : geometry_msgs/Twist

## 使用rosmsg查看消息的详细信息：
```
# e.g.
$ rosmsg show geometry_msgs/Twist
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
$ rostopic pub -1 /turtle1/cmd_vel geometry_msgs/Twist -- '[2.0, 0.0, 0.0]' '[0.0, 0.0, 1.8]'
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
$ rostopic hz [topic]
# e.g. 
$ rostopic hz /turtle1/pose
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
