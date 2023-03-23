rosparam能让我们在ROS参数服务器（Parameter Server）上存储和操作数据。参数服务器能够存储整型（integer）、浮点（float）、布尔（boolean）、字典（dictionaries）和列表（list）等数据类型。rosparam使用YAML标记语言的语法。一般而言，YAML的表述很自然：1是整型，1.0是浮点型，one是字符串，true是布尔型，[1, 2, 3]是整型组成的列表，{a: b, c: d}是字典。rosparam有很多命令可以用来操作参数，如下所示：
```
rosparam set            设置参数
rosparam get            获取参数
rosparam load           从文件中加载参数
rosparam dump           向文件中转储参数
rosparam delete         删除参数
rosparam list           列出参数名
```

### rosparam list
```
$ rosparam list
```

turtlesim节点在参数服务器上有3个参数用于设定背景颜色：
```
/rosdistro
/roslaunch/uris/host_nxt__43407
/rosversion
/run_id
/turtlesim/background_b
/turtlesim/background_g
/turtlesim/background_r
```

### sparam set和rosparam get的用法
```
$ rosparam set [param_name]
$ rosparam get [param_name]
```
```
# e.g.
$ rosparam set /turtlesim/background_r 150
# 上述指令修改了参数的值，现在我们需要调用clear服务使得参数的修改能生效：
$ rosservice call /clear
# 查看参数服务器上其他参数的值。获取背景的绿色通道的值：
$ rosparam get /turtlesim/background_g 
# 、或者可以用rosparam get /来显示参数服务器上的所有内容：
$ rosparam get /
```

### rosparam dump和rosparam load的用法
如果希望将参数保存在一个文件中，一边下次可以重新加载，可以使用rosparam实现：
```
$ rosparam dump [file_name] [namespace]
$ rosparam load [file_name] [namespace]
```
将所有的参数写入params.yaml文件：
```
$ rosparam dump params.yaml
```
或者将yaml文件重载入新的命名空间，例如copy_turtle：
```
$ rosparam load params.yaml copy_turtle
$ rosparam get /copy_turtle/turtlesim/background_b
```