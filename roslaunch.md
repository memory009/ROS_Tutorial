## 使用roslaunch
https://wiki.ros.org/cn/ROS/Tutorials/UsingRqtconsoleRoslaunch

用法：
```
$ roslaunch [package] [filename.launch]
```

open a new terminnal

```
$ cd ~/your_ws
$ source devel/setup.bash
$ roscd beginner_tutorials

# 如果没有这个beginner_tutorials的包，那么就用以下方法创建一个。
# 创建一个软件包，这将会创建一个名为beginner_tutorials的文件夹，这个文件夹里面包含一个package.xml文件和一个CMakeLists.txt文件，这两个文件都已经部分填写了你在执行catkin_create_pkg命令时提供的信息。
$ catkin_create_pkg beginner_tutorials std_msgs rospy roscpp
```
```
# catkin_create_pkg命令会要求你输入package_name，如有需要还可以在后面添加一些需要依赖的其它软件包：
# This is an example, do not try to run this
# catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
```

然后创建一个launch目录：
```
$ mkdir launch
$ cd launch
```


```
<launch>

  <group ns="turtlesim1">
    <node pkg="turtlesim" name="sim" type="turtlesim_node"/>
  </group>

  <group ns="turtlesim2">
    <node pkg="turtlesim" name="sim" type="turtlesim_node"/>
  </group>

  <node pkg="turtlesim" name="mimic" type="mimic">
    <remap from="input" to="turtlesim1/turtle1"/>
    <remap from="output" to="turtlesim2/turtle1"/>
  </node>

</launch>
```




解析：
* 首先用launch标签开头，以表明这是一个launch文件。
```
<launch>
```
* 此处我们创建了两个分组，并以命名空间（namespace）标签来区分，其中一个名为turtulesim1，另一个名为turtlesim2，两个分组中都有相同的名为sim的turtlesim节点。这样可以让我们同时启动两个turtlesim模拟器，而不会产生命名冲突。
```
  <group ns="turtlesim1">
    <node pkg="turtlesim" name="sim" type="turtlesim_node"/>
  </group>

  <group ns="turtlesim2">
    <node pkg="turtlesim" name="sim" type="turtlesim_node"/>
  </group>
```
  * 在这里我们启动模仿节点，话题的输入和输出分别重命名为turtlesim1和turtlesim2，这样就可以让turtlesim2模仿turtlesim1了。
```
  <node pkg="turtlesim" name="mimic" type="mimic">
    <remap from="input" to="turtlesim1/turtle1"/>
    <remap from="output" to="turtlesim2/turtle1"/>
  </node>
```
* 这一行使得launch文件的XML标签闭合。
```
</launch>
```