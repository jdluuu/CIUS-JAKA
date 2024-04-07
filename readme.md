# CIUS2024 机械臂动态重规划代码库

## 目录
### PartI Questions
### PartII Quick start
### PartIII 正常情况下文件夹的结构

## Update

注意，本次代码修改了以下部分

```
1. Cmakelist.txt
2. newcontroller.cpp
3. jakaUr/united_jakaUr_gazebo/launch/posi_only.launch
4. jakaUr/united_jakaUr_gazebo/launch/arm_gazebo_controller.launch
5. jakaUr/united_jakaUr_gazebo/config/arm_cam_joint.yaml
6. jakaUr/united_jakaUr_gazebo/config/arm_gazebo_control.yaml
```

同时，cam_follow.py也有很小的修改：
```
joint1_controller -> cam_joint1_controller
joint2_controller -> cam_joint2_controller
```

现在应该使用以下代码启动控制器：

```
roslaunch united_jakaUr_gazebo posi_only.launch
rosrun myController newcontroller
```



## PartI Questions

存在已知的问题，控制器有可能卡死或者规划失败，问题根据我目前的认知来自于轨迹重规划使用的时间具有不确定性，以及ros自身消息传递有延迟，已经在改了=.=

## PartII Quick start
### 依赖:
ubuntu 18.04 + ros melodic

realsence SDK

pcl(ros自带的应该就可以)


### 如何运行：

新建ros工作空间，将所有的文件夹都放在src下。

```
mkdir -p jiadong_ws/src
cd jiadong_ws/src
catkin_init_workspace

# copy files
cd ..
catkin_make
source devel/setup.bash
```

### 进行gazbeo仿真：

```
roslaunch united_jakaUr_gazebo arm_bringup_moveit.launch
```

### 进行摄像头跟踪：
```
python cam_follow.py
```

### 进行点云处理：
```
rosrun pcl_try receive
```

### 进行往返运动：
```
rosrun myController controller
```

### 添加一个小立方体在路径上：
建议小立方体在机械臂要从初始点出来的时候添加，因为这个摄像头不是广角，随便添加的话有可能扫描不到，然后规划失败=.=。远一点的话就没问题了。
```
roslaunch united_jakaUr_gazebo load_box.launch
```

## Part III 正常请况下文件夹的结构
```
├── src
│   ├── CMakeLists.txt -> /opt/ros/melodic/share/catkin/cmake/toplevel.cmake
│   ├── jakaUr
│   ├── jakaUr_ikfast
│   ├── myController
│   ├── pcl_try
│   ├── realsense_gazebo_plugin
│   ├── realsense-ros
│   └── worlds
└── cam_follow.py
