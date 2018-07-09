rb2_sim
=============

Packages for the simulation of the RB-2 Base

<p align="center">
  <img src="https://www.robotnik.es/logistics/portfolio/rb-2-base-2/"/>
</p>


<h1> Packages </h1>

<h2>rb2_gazebo</h2>

This package contains the configuration files and worlds to launch the Gazebo environment along with the simulated robot.

<h2>rb2_sim_bringup</h2>

Launch files that launch the complete simulation of the robot/s.



<h1>Simulating RB-2 </h1>

1. Install the following dependencies:
  - rb2_common [link](https://github.com/RobotnikAutomation/rb2_common)
  - robotnik_msgs [link](https://github.com/RobotnikAutomation/robotnik_msgs)
  - robotnik_sensors [link](https://github.com/RobotnikAutomation/robotnik_sensors)

    In the workspace install the packages dependencies:
    ```
    rosdep install --from-paths src --ignore-src -r -y
    ```  

2. Launch RB-2  simulation (1 robot by default, up to 3 robots): <br>
- RB-2 Base: <br>
  ```
  roslaunch rb2_sim_bringup rb2_complete.launch
  ```

  Optional general arguments:
  ```
  <arg name="launch_rviz" default="true"/>
  <arg name="gazebo_world" default="$(find rb2_gazebo)/worlds/rb2_office.world"/>

  ```
  Optional robot arguments:
  ```
  <!--arguments for each robot (example for robot A)-->
  <arg name="id_robot_a" default="rb2_a"/>
  <arg name="launch_robot_a" default="true"/>
  <arg name="map_file_a" default="$(find rb2_localization)/maps/willow_garage/willow_garage.yaml""/>
  <arg name="localization_robot_a" default="true"/>
  <arg name="gmapping_robot_a" default="false"/>
  <arg name="move_base_robot_a" default="false"/>
  <arg name="amcl_and_mapserver_a" default="false"/>
  <arg name="x_init_pose_robot_a" default="0" />
  <arg name="y_init_pose_robot_a" default="0" />
  <arg name="z_init_pose_robot_a" default="0" />
  <arg name="xacro_robot_a" default="rb2_std.urdf.xacro"/>
  <arg name="map_frame_a" default="$(arg id_robot_a)_map"/>
  ```
- Example to launch simulation with 3 RB-2 Base robots:
  ```
  roslaunch rb2_sim_bringup rb2_complete.launch launch_robot_b:=true launch_robot_c:=true
  ```
- Example to launch simulation with 1 RB-2 Base robot with navigation and localization:
  ```
  roslaunch rb2_sim_bringup rb2_complete.launch move_base_robot_a:=true amcl_and_mapserver_a:=true
  ```
- Example to launch simulation with 2 RB-2 Base robot with navigation and localization sharing the same global frame:
  ```
  roslaunch rb2_sim_bringup rb2_complete.launch amcl_and_mapserver_a:=true move_base_robot_a:=true map_frame_a:=/map launch_robot_b:=true amcl_and_mapserver_b:=true move_base_robot_b:=true map_frame_b:=/map
  ```
- Example to launch simulation with 3 RB-2 Base robot with navigation and localization sharing the same global frame:
```
roslaunch rb2_sim_bringup rb2_complete.launch amcl_and_mapserver_a:=true move_base_robot_a:=true map_frame_a:=/map launch_robot_b:=true amcl_and_mapserver_b:=true move_base_robot_b:=true map_frame_b:=/map launch_robot_c:=true amcl_and_mapserver_c:=true move_base_robot_c:=true map_frame_c:=/map
```
3. Enjoy! You can use the topic "${id_robot}/robotnik_base_control/cmd_vel" to control the RB-2 Base robot or send simple goals using "/${id_robot}/move_base_simple/goal"
