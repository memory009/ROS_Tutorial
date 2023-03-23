## 文件管理工具
### 使用rospack
```
$ rospack find [package_name]
# it will output: YOUR_INSTALL_PATH/share/roscpp
```
### 使用roscd
```
$ roscd [locationname[/subdir]]
# output the working directory
$ pwd
```
注意，就像ROS中的其它工具一样，roscd只能切换到那些路径已经包含在ROS_PACKAGE_PATH环境变量中的软件包。要查看 ROS_PACKAGE_PATH中包含的路径，可以输入：
```
$ echo $ROS_PACKAGE_PATH
```