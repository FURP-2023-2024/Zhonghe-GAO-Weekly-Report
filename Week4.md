## Parameters of Navigation
**·Move_base**

shutdown_costmaps: false

This parameter controls whether costmaps are shut down when the robot stops moving. Costmaps are maps showing environmental information around the robot, including obstacles and navigable paths. Here, false means costmaps won't automatically shut down when the robot stops, keeping them active for future navigation.

controller_frequency: 10.0

Controller frequency dictates how many times per second the controller executes. Here, the controller executes at a rate of 10 times per second for path tracking and motion control.

planner_patience: 5.0

Planner patience specifies the number of consecutive planning failures the planner tolerates. If planning fails consecutively more than 5 times, move_base considers executing recovery behaviors.

controller_patience: 15.0

Controller patience defines the number of consecutive path tracking failures the controller tolerates. If path tracking fails consecutively more than 15 times, move_base considers executing recovery behaviors.

conservative_reset_dist: 3.0

Conservative reset distance specifies the minimum distance the robot should move during recovery behaviors. For instance, if the robot encounters issues during planning or path tracking, it might move at least 3 meters to attempt re-planning or re-tracking the path.

planner_frequency: 5.0

Planner frequency dictates how many times per second the planner executes global path planning. Here, the planner executes at a rate of 5 times per second for global path planning.

oscillation_timeout: 10.0

Oscillation timeout defines the time limit for detecting oscillatory behavior, where the robot repeats similar movements within a specified time frame. If the robot oscillates persistently for 10 seconds, move_base may execute recovery behaviors to correct its motion.

oscillation_distance: 0.2

Oscillation distance threshold specifies the minimum distance used to detect oscillatory behavior. If the robot moves back and forth within 0.2 meters, the system may identify it as oscillating.
These parameters significantly influence the navigation behavior and performance of the robot. Adjusting these parameters can optimize path planning and path tracking during navigation, enhancing the robot's capability to navigate through complex environments effectively.

**·Global Costmap**

global_frame: map

The `global_frame` specifies the coordinate system used by the global costmap. Here, `map` indicates that the data of the global costmap will be represented and processed in the coordinate system named "map."

robot_base_frame: base_footprint

The `robot_base_frame` specifies the coordinate system of the robot's body. Here, `base_footprint` represents the robot's base coordinate system, which serves as the reference for the robot's movement.

update_frequency: 10.0

The `update_frequency` defines the update frequency of the global costmap, that is, the number of updates per second. Here, a setting of `10.0` means that the global costmap updates 10 times per second.

publish_frequency: 10.0

The `publish_frequency` defines the frequency at which the global costmap publishes updates, that is, the number of updates published per second. Similar to `update_frequency`, here it is set to `10.0`, meaning updates are published 10 times per second.

transform_tolerance: 0.5

The `transform_tolerance` defines the maximum waiting time before receiving transform updates. This parameter ensures that the global costmap can remain stable for a certain period before receiving the latest transform data.

static_map: true

The `static_map` specifies whether to use a static map as the basis for the global costmap. A static map is usually a pre-built environment map that contains information about static obstacles. Here, setting it to `true` means that the global costmap uses a static map.

The settings of these parameters affect the functionality and performance of the global costmap in ROS navigation, ensuring that the robot can accurately perceive the environment and perform path planning to achieve safe and efficient navigation.

Local Costmap

**global_frame: odom**

The `global_frame` specifies the global coordinate system used by the local costmap. Here, `odom` indicates that the data of the local costmap will be represented and processed in the coordinate system named "odom." This differs from the global costmap, which typically uses the `map` coordinate system, as `odom` is closer to the robot's motion trajectory rather than the entire map.

robot_base_frame: base_footprint

The `robot_base_frame` specifies the coordinate system of the robot's body, similar to the setting in the global costmap. Here, `base_footprint` represents the coordinate system of the robot's base, which serves as the reference for the robot's movement.

update_frequency: 10.0

The `update_frequency` defines the update frequency of the local costmap, indicating the number of updates per second. Here, a setting of `10.0` means the local costmap updates 10 times per second.

publish_frequency: 10.0

The `publish_frequency` defines how often the local costmap publishes updates, measured in updates per second. Similar to `update_frequency`, it is set to `10.0`, meaning updates are published 10 times per second.

transform_tolerance: 0.5

The `transform_tolerance` defines the maximum wait time before receiving transform updates. This parameter ensures the local costmap remains stable for a certain period before receiving the latest transform data.

static_map: false

The `static_map` specifies whether to use a static map as the basis for the local costmap. Here, setting it to `false` means the local costmap does not use a static map. In contrast, the global costmap typically uses a static map for long-term path planning, while the local costmap focuses more on real-time environment perception and dynamic obstacle avoidance.

rolling_window: true

The `rolling_window` defines whether to enable the rolling window mode for constructing the local costmap. This mode allows the local costmap to dynamically update with the robot's movement, focusing only on a small surrounding area of the robot.

width: 3

The `width` defines the width of the local costmap in grid units. Here, setting it to `3` means the local costmap updates and perceives within a width of 3 grid units around the robot.

height: 3

The `height` defines the height of the local costmap in grid units. Setting it to `3` means the local costmap updates and perceives within a height of 3 grid units around the robot.

resolution: 0.05

The `resolution` defines the resolution of the costmap, indicating the size of each grid cell. Here, setting it to `0.05` means each grid cell has a side length of 0.05 meters, determining the perception accuracy of the costmap for environmental details.

These parameters affect the functionality and performance of the local costmap in ROS navigation, ensuring the robot can effectively perceive its immediate surroundings and perform real-time obstacle avoidance.

**Dynamic Writing Approach Planner**

1. Robot Configuration Parameters
   - `max_vel_x`: Maximum linear velocity of the robot along the x-axis (forward direction), in meters per second (m/s).
   - `min_vel_x`: Minimum linear velocity of the robot along the x-axis.
   - `max_vel_y`, `min_vel_y`: Maximum and minimum linear velocities of the robot along the y-axis (lateral movement direction), typically 0 indicating no lateral movement allowed.
   - `max_vel_trans`, `min_vel_trans`: Maximum and minimum translational velocities of the robot, i.e., speed when moving straight in meters per second.

2. Goal Tolerance Parameters:
   - `xy_goal_tolerance`: Tolerance in the xy plane allowed when reaching the goal position, in meters.
   - `yaw_goal_tolerance`: Tolerance in yaw angle allowed when reaching the goal position, in radians.
   - `latch_xy_goal_tolerance`: Whether to latch the xy goal tolerance.

3. Forward Simulation Parameters:
   - `sim_time`: Time horizon for forward simulation, used by the planner to evaluate potential paths, in seconds.
   - `vx_samples`, `vy_samples`, `vth_samples`: Number of velocity samples generated during forward simulation for linear and angular velocities.
   - `controller_frequency`: Frequency of the controller updates, in Hertz.

4. Trajectory Scoring Parameters:
   - `path_distance_bias`: Bias towards path distance, influencing how much emphasis is placed on path length during path selection.
   - `goal_distance_bias`: Bias towards goal distance, influencing how much emphasis is placed on distance to the goal during path selection.
   - `occdist_scale`: Scale for occupancy grid distance, weighting factor to avoid collisions.
   - `forward_point_distance`: Distance between forward points used in trajectory generation.
   - `stop_time_buffer`: Time buffer when stopping in path planning.
   - `scaling_speed`, `max_scaling_factor`: Speed of path scaling and maximum scaling factor.

5. Oscillation Prevention Parameters:
   - `oscillation_reset_dist`: Distance threshold for oscillation reset, used to reset the path when the robot oscillates.

6. Debugging:
   - `publish_traj_pc`: Whether to publish trajectory point cloud for debugging.
   - `publish_cost_grid_pc`: Whether to publish cost grid point cloud for debugging.

**Trajectory Planner** 
Robot Configuration Parameters
max_vel_x: Maximum linear velocity of the robot along the x-axis (forward direction), in meters per second (m/s).
min_vel_x: Minimum linear velocity of the robot along the x-axis, in meters per second (m/s).
max_vel_theta: Maximum angular velocity of the robot around the z-axis (yaw), in radians per second (rad/s).
min_vel_theta: Minimum angular velocity of the robot around the z-axis (yaw), in radians per second (rad/s).
min_in_place_vel_theta: Minimum angular velocity for in-place rotation, in radians per second (rad/s).
acc_lim_x: Acceleration limit of the robot along the x-axis, in meters per second squared (m/s²).
acc_lim_y: Acceleration limit of the robot along the y-axis, typically 0 indicating no lateral acceleration.
acc_lim_theta: Acceleration limit of the robot around the z-axis (yaw), in radians per second squared (rad/s²).
Goal Tolerance Parameters
xy_goal_tolerance: Tolerance in the xy plane allowed when reaching the goal position, in meters.
yaw_goal_tolerance: Tolerance in yaw angle allowed when reaching the goal position, in radians.
Differential-drive robot configuration
holonomic_robot: Whether the robot is holonomic (true) or non-holonomic (false). Holonomic robots can move in any direction, while non-holonomic robots can only move along the forward direction.
Forward Simulation Parameters
sim_time: Time horizon for forward simulation used by the planner to evaluate potential paths, in seconds.
vx_samples: Number of linear velocity samples generated during forward simulation.
vtheta_samples: Number of angular velocity samples generated during forward simulation.
sim_granularity: Granularity or resolution of the forward simulation, used for path generation, in meters.

**Costmap Common**

Range Parameters
obstacle_range: Obstacle range, in meters (m). Objects detected by the sensor within this range will be considered as obstacles.
raytrace_range: Ray tracing range, in meters (m). This is the maximum range of the sensor used for clearing obstacle information from the costmap.

Footprint Parameters
footprint: A list of vertex coordinates defining the robot's physical shape and size. Each point represents a vertex coordinate of the robot's footprint in the 2D plane. The example footprint is a quadrilateral with vertex coordinates [-0.105, -0.105], [-0.105, 0.105], [0.041, 0.105], [0.041, -0.105].
robot_radius: The radius of the robot, in meters (m). This parameter is usually used to define a circular robot footprint but is commented out here, indicating the use of the polygon footprint above.

Inflation Parameters
inflation_radius: Inflation radius, in meters (m). This defines the inflated area around obstacles in the costmap to ensure the robot maintains a safe distance during navigation.
cost_scaling_factor: Cost scaling factor, which controls the rate of cost increase in the inflation area. The larger the value, the faster the cost increases.

Map Parameters
map_type: The type of map. In this example, it is set to costmap, indicating the use of a costmap.
observation_sources: A list of observation sources that provide environmental data for updating the costmap. Here, an observation source named scan is set.

Sensor Parameters
scan: Configures a laser scan sensor named scan.
sensor_frame: The coordinate frame of the sensor, here it is base_scan.
data_type: The type of sensor data, here it is LaserScan, indicating laser scan data.
topic: The topic for sensor data, here it is scan.
marking: Set to true, indicating that sensor data is used for marking obstacles.
clearing: Set to true, indicating that sensor data is used for clearing obstacle information.
