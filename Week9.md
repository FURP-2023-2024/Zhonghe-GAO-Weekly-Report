## Week 9 Map Building and Auto Navigation
### Week 9 Overview
Week 9 has been a remarkably productive week. We successfully set up the navigation stack and utilized te Cartographer algorithhm to complete the map construction of IAMET_L2, achieveing a certain degree of navigation functionality.
In this repo, the navigation package is shown with the related launch and config files.
### Navigation Package
- [roborts_base](https://github.com/FURP-2023-2024/Zhonghe-GAO-Weekly-Report/blob/main/base.launch)
  
   This package is located in catkin_ws, which including a launch file named as base.launch. This launch file could start the chassis and publish **/odom** topic.
- [rplidar_ros](https://github.com/FURP-2023-2024/Zhonghe-GAO-Weekly-Report/blob/main/rplidar_a2m8.launch)

  The launch file in the "rpliidar" workspace called as rplidar_a2m8.launch is used to start laser and publish the **/scan** topic.
- cartographer

  In order to build the map, cartographer, as one of a SLAM algorithm, is deployed through adding [cartographer.launch](https://github.com/FURP-2023-2024/Zhonghe-GAO-Weekly-Report/blob/main/cartographer.launch)  and [cartograper_config.lua](https://github.com/FURP-2023-2024/Zhonghe-GAO-Weekly-Report/blob/main/cartographer_config.lua). 
- my_navigation_pkg
  The navigation stack is established in this package with the  [move_base.launch](https://github.com/FURP-2023-2024/Zhonghe-GAO-Weekly-Report/blob/main/move_base.launch) and other related config files, including [move_base.yaml](https://github.com/FURP-2023-2024/Zhonghe-GAO-Weekly-Report/blob/main/move_base.yaml), [global_cost_map.yaml](https://github.com/FURP-2023-2024/Zhonghe-GAO-Weekly-Report/blob/main/global_costmap.yaml), [local_cost_map.yaml](https://github.com/FURP-2023-2024/Zhonghe-GAO-Weekly-Report/blob/main/local_costmap.yaml), [planner.yaml](https://github.com/FURP-2023-2024/Zhonghe-GAO-Weekly-Report/blob/main/planner.yaml), and [amcl.yaml](https://github.com/FURP-2023-2024/Zhonghe-GAO-Weekly-Report/blob/main/planner.yaml).
### Results and Discussion
- Map of IAMET_L2

<img width="368" alt="IAMET_L2" src="https://github.com/user-attachments/assets/3e547688-7fc5-4ac4-8087-740828c8a877">


- Visulaized information on Rviz


- Actual Navigation Performance 

Overall navigation performance is suboptimal, primarily due to the following issues:

 - Failure to avoid obstacles; the robot cannot autonomously navigate around obstacles.
 - Uncontrolled backward movements and spinning in place occur.
 - Shorter-than-expected travel distances when using the 2D Navigation Goal function.
 - Abnormal odometry readings, exceeding the map boundaries.





