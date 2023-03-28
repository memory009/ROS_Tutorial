## ROS多机通讯&yahboomcar实战
### 多机通讯
* 个人电脑ssh与小车建立通讯
```
$ ssh jetson@192.168.xx.xxx(master机ip)
$ password:yahboom
```

### ROS多机通讯
#### 主机
* 机器ip可通过ifconfig查看
```
# step_1
$ export ROS_MASTER_URI=http://192.168.xx.xxx:11311(master机ip)

# step_2
$ export ROS_HOSTNAME=192.168.xx.xxx(本机ip)
# or
export ROS_IP=192.168.xx.xxx(本机ip)
```

#### 从机
```
# step_1
$ export ROS_MASTER_URI=http://192.168.xx.xxx:11311(master机ip)

# step_2
$ export ROS_HOSTNAME=192.168.xx.xxx(本机ip)
# or
export ROS_IP=192.168.xx.xxx(本机ip)

```

### 实战
* 启动小车底盘& 3D laser
```
# 在jeston@SSD的terminnal
$ roslaunch yahboomcar_nav 3d_laser_bringup.launch
```

* 启动导航
```
# 在jeston@SSD的terminnal
$ roslaunch yahboomcar_nav yahboomcar_navigation.launch
```

* 在从机调用rviz监控小车的情况（可有效解决额VNC带来的远程控制延迟问题）
```
# 在本机
$ export...(详见多机通讯从机step1&2)
$ cd ~/yahboomcar_ws(?)
$ source devel/setup.bash
$ roslaunch yahboomcar_nav view_navigate.launch
```

* 实时调整参数（不会影响小车原文件）
```
# 在本机
$ export...(详见多机通讯从机step1&2)
$ rosrun rqt_reconfigure rqt_reconfigure
```