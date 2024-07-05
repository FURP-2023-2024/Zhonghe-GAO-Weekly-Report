## Week 3

In this week, we mainly use Turtlebot with Gazebo and Rviz to do with mapping and navigation. 
Here are some key steps:

**Step1:** Open the robot and the gazebo platform

```export TURTLEBOT3_MODEL=waffle```

```roslaunch turtlebot3_gazebo turtlebot3_house.launch```

**Step2:** Applying cartographer algorithm to gazebo

```export TURTLEBOT3_MODEL=waffle```

```roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=cartographer```

**Step3:** Use keypad to control the movement of robot

```export TURTLEBOT3_MODEL=waffle```

```roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch```

**Step4**:  Reserve the map.
<img width="415" alt="image" src="https://github.com/FURP-2023-2024/Zhonghe-GAO-Weekly-Report/assets/172378135/0551e4f1-09e3-4bdb-8417-127c13f62689">

