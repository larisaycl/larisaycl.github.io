---
title: "Feature-based Kalman Filter SLAM in ROS"
excerpt: "ROS implementation of SLAM using an extended kalman filter<br/><img src='/images/portfolio-slam/side_view.png'>"
collection: portfolio
---

## Overview
This project was done as a collection of homework assignments for ME 495 Sensing, Navigation, and Machine Learning For Robotics at Northwestern. The task was to build a several ROS packages to implement control and SLAM (simultaneous localization and mapping) for a turtlebot3 burger robot. The repo is not made available since this is class homework.

## Package list
This repository consists of several ROS packages. 
* `nuturtle_description` - contains URDF files, meshes, and launch file for launching and displaying the turtlebot3 burger in rviz.
* `rigid2d` - a package for odometry of a differential drive robot, with a library for rigid body transformations in SE(2),
* `trect` - a package for controlling a turtlesim turtle to move along a rectangular path.
* `nuturtle_robot` - a package for interfacing with a physical turtlebot3 burger robot. Contains launch files for launching remote nodes, and the `turtle_interface_node` for low-level commands.
* `nurtlesim` - a package that provides a simulator for the turtlebot and SLAM in rviz
* `nuslam` - a package that implements Feature-Based Kalman Filter SLAM for the turtlebot.

## Description of packages

### `rigid2d` - Rigid 2D transformation Library
A library for handling transformations in SE(2), as well as handling odometry calculations for a differential drive robot. See [this document](/files/diff_drive.pdf) for derivations of equations used in the `diff_drive.cpp` library implementation file.

Library implementation files 
- `rigid2d.cpp`
   - usage: include `rigid2d/rigid2d.hpp`
   - 2D rigid body transformations
- `diff_drive.cpp` 
   - usage: include `rigid2d/diff_drive.hpp`
   - kinematics of a differential drive robot

Nodes
* `rigid2d_fake_turtle_node` in `fake_turtle.cpp`
* `rigid2d_odometer_node` in `odometer.cpp`


### `nuturtle_robot` - turtlebot3 low-level controller
This package provides functionality to interface with low-level commands on the turtlebot, as well as launch files to start basic nodes on the turtlebot to allow interfacing with ROS. 

<!-- ### Pure translation test
After moving forwards and backwards several times and stopping at the initial position, the odometry location of the robot was (6.328e-04, 5.219e-03, 9.759e-04).   
![translation_screen](/images/portfolio-slam/F81screen.gif)
![translation_turtle](/images/portfolio-slam/F81turtle.gif)

### Driving at maximum speed
The pure translation experiment was repeated, this time driving at maximum speed (0.22 m/s) as compared to 0.09m/s in the first experiment. The results of the location in odometry are much less accurate in this case. The turtlebot also was not able to move in a straight path at such high speeds, likely due in part to differences in the motor speeds and tyre friction. The final odometry location of the robot was (0.119, 6.644e-02, -8.248e-03).    
![translation_screen_fast](/images/portfolio-slam/F84screen.gif)
![translation_turtle_fast](/images/portfolio-slam/F84turtle.gif)

### Pure rotation test
After rotating clockwise and counterclockwise several times and stopping at the initial position, the odometry location of the robot was (9.491e-04, -1.930e-06, 2.018e-05).      
![rotation_screen](/images/portfolio-slam/F82screen.gif)
![rotation_turtle](/images/portfolio-slam/F82turtle.gif) -->

Circle path test
After following a clockwise and counterclockwise circluar path several times and stopping at the initial position, the odometry location of the robot was (0.2667, 0.13376, -3.683e-03).     
![circle_screen](/images/portfolio-slam/F83screen.gif)
![circle_turtle](/images/portfolio-slam/F83turtle.gif)


### `nurtlesim` - simulator for turtlebot3 burger in tube world in rviz
This packages provides a simulator for the turtlebot and slam in rviz.
The simulator simulates the robot kinematics and a sensor that detects the relative x, y positions of landmarks and a landmark id. Landmarks are modelled as tubes (approx 10cm diameter cylinders).

### `nuslam` - Feature-based SLAM
This package implements Feature-Based Kalman Filter SLAM for a turtlebot in the `nurtlesim` simulation. It also provides a library for handling the SLAM algorithm calculations for a differential drive robot. 

Library implementation files
- `nuslam_lib.cpp`
    - usage: include `nuslam/nuslam_lib.hpp`
    - Feature-based Kalman Filter SLAM calculation helper functions 
    - Data association using mahalanobis distance 
    - A maximum of 10 landmarks can be stored
- `circle_fitting.cpp`
    - usage: include `nuslam/circle_fitting.hpp`
    - Circle fitting with circle regression
    - Circle classification

Nodes
- `nuslam_node` in `slam.cpp` - SLAM with known data association
- `landmarks_node` in `landmarks.cpp` - circle fitting and classification
- `nuslam_unknown_node` in `slam_unknown.cpp` - SLAM with unknown data association

Demonstration SLAM with known data association
- The robot was driven around in simulation such that all the landmarks were encountered during the run.
- ground truth landmarks are shown in white
- landmarks detected by the sensor are shown in red
- landmarks according to slam (the map) are shown in blue
- trajectory of the actual robot is shown in green
- trajectory of the robot according to SLAM is shown in orange
- trajectory of the robot according to odometry is shown in white
- turtle (actual turtle position frame)       

The result for default R and Q is shown:     

Top view:        
![top_view](/images/portfolio-slam/top_view.png)

Perspective view:        
![side_view](/images/portfolio-slam/side_view.png)

<!-- ---

#### Slam with unknown data association
The robot was driven around in simulation such that all the landmarks were encountered during the run.
- robot is driven at max linear speed 0.01m/s and max angular speed 0.1rad/s
- ground truth landmarks are shown in white
- landmarks detected by the sensor are shown in red
- landmarks according to slam (the map) are shown in blue
- trajectory of the actual robot is shown in green
- trajectory of the robot according to SLAM is shown in orange
- trajectory of the robot according to odometry is shown in white
- turtle (actual turtle position frame)     

A screencast of the robot driving around in the environment is shown:
![unknown_data_assoc_demo1](/images/portfolio-slam/slam_unknown_demo1.gif)

A screencast of the robot driving around in the environment is shown:
![unknown_data_assoc_demo2](/images/portfolio-slam/slam_unknown_demo2.gif) -->