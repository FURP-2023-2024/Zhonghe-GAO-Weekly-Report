## Week 9 Map Building and Auto Navigation
### Week 9 Overview
Week 9 has been a remarkably productive week. We successfully set up the navigation stack and utilized te Cartographer algorithhm to complete the map construction of IAMET_L2, achieveing a certain degree of navigation functionality.
In this repo, the navigation package is shown with the related launch and config files.
### Navigation Package
- roborts_base
  
   This package is located in catkin_ws, which including a launch file named as base.launch. This launch file could start the chassis and publish **/odom** topic.
- rplidar_ros

  The launch file in the "rpliidar" workspace called as rplidar_a2m8.launch is used to start laser and publish the **/scan** topic.
- cartographer

  In order to build the map, cartographer, as one of a SLAM algorithm, is deployed through adding cartographer.launch  and cartograper_config.lua . 
- my_navigation_pkg
  The navigation stack is established in this package with the  move_base.launch and other related config files, including move_base.yaml, global_cost_map.yaml, local_cost_map.yaml, planner.yaml, and amcl.yaml.
### Results and Discussion
- Map of IAMET_L2

<img width="368" alt="IAMET_L2" src="https://github.com/user-attachments/assets/3e547688-7fc5-4ac4-8087-740828c8a877">


