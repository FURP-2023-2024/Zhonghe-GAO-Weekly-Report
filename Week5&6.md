## Week 5&6 Unitree Go 1 Simulation and Control
In these two weeks, we achieved the Gazebo simulation and control of Unitree Go 1 robot.
### Package Installation
```
unitree_ros: Mainly used to simulation, such as rviz and gazebo.
unitree_ros_to_real:corresponding electrical machines and speed.
unitree_legged_sdk: communication and robotic movement, contributing to actual control.
unitree_guide
```
### Gzebo Simulation
Open the Gazebo
```
roslaunch unitree_guide gazeboSim.launch
```
Start the controller
```
rosrun unitree_guide junior_ctrl
```
Note: Some references mention the following command to start the controller. However, in my computer, this doesn't work.
```
sudo ./devel/lib/unitree_guide_junior_ctrl
```
![463433258282943959](https://github.com/user-attachments/assets/aa4b9e13-4222-436e-a1bf-9458d3954149)
![265482381649628018](https://github.com/user-attachments/assets/9e3dadc3-194e-4371-a7a3-9a7362590334)
## Real Robot Control 
1. Configuring the robot's Raspberry pi with the user's computer netwrok, enabling the real time control.
2. Change the code to real robot mode.
In CMakeLists.txt
```
SIMULATION OFF
REAL_ROBOT ON
```
In the new terminal
```
rosrun unitree_guided junior_ctrl
```






