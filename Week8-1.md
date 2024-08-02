## Navigation Pakcage Configuration 
This week we tried mmany methods to configure a navigation package. 
Our main idea was that a navigation package should include: 
1. Node of robot base control
2. Node of Slam
3. Move_base package

This is our first launch file:
### Create a launch file to achieve the robot's auto navigation
```
<launch>
    <!-- 启动底盘控制节点 -->
    <node pkg="robort_base" type="roborts_base_node" name="roborts_base_node"/>


    <!-- 启动Cartographer SLAM节点 -->
    <include file="$(find catkin_ws_cartographer)/launch/cartographer.launch"/>

    <!-- 加载地图 -->
    <arg name="map_file" default="$(find my_robot_maps)/maps/my_map.yaml"/>
    <node name="map_server" pkg="map_server" type="map_server" args="$(arg map_file)"/>

    <!-- 启动move_base -->
    <include file="$(find move_base)/launch/move_base.launch">
        <!-- 配置move_base，使用适合全向机器人的路径规划器 -->
        <arg name="base_local_planner" value="dwa_local_planner/DWAPlannerROS"/>
    </include>
</launch>
```
**However, nothing works**
Then we want to apply the navgation package of turtlebot.
Although we know how to deal with , not too much.
In conclusion, we tried a lot of methods to build the navigation package of our robot, however, **nothing works**.


