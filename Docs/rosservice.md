## how to use rosservice
rosservice可以很容易地通过服务附加到ROS客户端/服务器框架上。rosservice有许多可用于服务的命令，如下所示：
```
rosservice list         输出活跃服务的信息
rosservice call         用给定的参数调用服务
rosservice type         输出服务的类型
rosservice find         按服务的类型查找服务
rosservice uri          输出服务的ROSRPC uri
```

### rosservice list
```
$ rosservice list
```
ist命令显示turtlesim节点提供了9个服务:
```
/clear
/kill
/reset
/rosout/get_loggers
/rosout/set_logger_level
/spawn
/teleop_turtle/get_loggers
/teleop_turtle/set_logger_level
/turtle1/set_pen
/turtle1/teleport_absolute
/turtle1/teleport_relative
/turtlesim/get_loggers
/turtlesim/set_logger_level
```

### rosservice type
TO DO

how to use
```
$ rosservice call [service] [args]
```
e.g.
```
# because the type of service is empty，so make a parameterless call：
rosservice call /clear
# when call the turtle's demo, if you run the above command, the previous track will be clear:
```

服务具有参数的情况。查看spawn服务的信息：
```
$ rosservice type /spawn | rossrv show
```
output:
```
float32 x
float32 y
float32 theta
string name
---
string name
```

this service can spawn a new turtle in given location&angle.The "name" field is optional,in this tutorial, I didn't set a given name, so turtlesim will create a name automatically.
```
$ rosservice call /spawn 2 2 0.2 "" # it will spawn a new turtle in
x = 2 
y = 2
theta = 0.2
```

该调用返回了新产生的乌龟的名字：
```
name: turtle2
```
