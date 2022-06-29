# Multirobot-Navigation

## Overview

This ROS package implements navigation for multiple robots autonomously. Initially, Simultaneous Localization and Mapping (SLAM) is used to map the unknown environment. Once the environment is mapped and the map is generated, multiple robots are navigated autonomously on the map using the ROS Navigation Stack. 

## Installation

Build from source, clone from this repository into your catkin workspace and compile the package using:
  
    git clone https://github.com/saiv20/multirobot_tb.git
    cd ..
    catkin_make

## Simultaneous Localization and Mapping (SLAM)

Simultaneous Localization and Mapping (SLAM) is implemented using slam_gmapping. The robot is spawed on Gazebo and we can move the robot around in the Gazebo environment.  

1. Launch Gazebo and spawn the robot in Gazebo environment. This launches with the world file `world1` in the worlds directory. Then, the `slam_gmapping` node is launched. RViz is also launched, which can be used to visualize the map being created.

	    roslaunch multirobot_tb gmapping.launch

2. Once the robot is spawned, we now proceed to moving the robot around the Gazebo environment. As we move the robot along the environment, we notice that the RViz map is simultaneously being updated. Keep moving the robot around the environment until a satisfactory map is obtained. 

	    roslaunch multirobot_tb teleop.launch
            
3. Once a satisfactory map is obtained, save the map and copy the map to `~/multirobot_tb/maps/` directory.
	      
        rosrun map_server map_saver -f ~/map_one
  
## Navigation of Multiple Robots

Once the map is generated, we can proceed to the navigation of multiple robots. This is achieved using the ROS Navigation Stack.  

1. Launch Gazebo and spawn multiple robots in Gazebo environment. Here, we are spawning 3 robots.

	    roslaunch multirobot_tb main.launch

2. Now we launch the rviz, move_base, and amcl nodes 

	    roslaunch multirobot_tb navigation.launch
            
3. In RViz, set the 2D Pose estimate topic to `/robot1/initialpose`. Once the topics are assigned, set the initial pose estimate of the robot by clicking on **2D Pose Estimate**. Similarly for the second robot, set the 2D Pose estimate topic to `/robot2/initialpose`. Follow the steps and assign the initial pose estimate of all robots by replacing robot1 with the name of the robot.

4. Set the 2D Nav Goal Topic to `/robot1/move_base_simple/goal` and click on **2D Nav Goal** and set the goal location and pose to move robot1. To move robot2, follow the same step by replacing robot1 with robot2 in 2D Nav Goal Topic. Repeat the steps for other robots by replacing robot1 with the name of the robot. This will move the corresponding robot to its goal location and pose.
  
  
