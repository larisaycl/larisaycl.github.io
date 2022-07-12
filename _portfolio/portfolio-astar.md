---
title: "A* Search for robot planning and navigation"
excerpt: "A* Search in Python for wheeled mobile robot path planning<br/><img src='/images/portfolio-astar/astar-coarse.png'>"
collection: portfolio
---

## Overview
This project was done as a homework assignment of CS/ME 469 ML and AI for Robotics at Northwestern. The task was to implement A* search from scratch to enable a wheeled mobile robot to navigate a gridworld with obstacles. Code is not provided since this is a regular homework assignment. 

## The grid world environment
Two gridworld environments of different discretization coarseness were built and used for testing. 

![](/images/portfolio-astar/astar-gw.png)

## Planning with A*
Results from planning in the coarse gridworld are shown:

![](/images/portfolio-astar/astar-coarse.png)

Results from planning in the fine gridworld are shown:

![](/images/portfolio-astar/astar-fine.png)

## Driving planned paths
A feedforward + feedback controller was built to simulate a differential drive robot driving the planned paths. Here is an example of the driven paths:

![](/images/portfolio-astar/astar-drive.png)

## Online planning
Planning-while-driving was tested. In the previous section, paths were pre-computed, after which the simulated robot would traverse the path. In this section, the robot takes a step and needs to re-plan based on the actual step that it has taken, since the robot controller might drive the robot into cells which are not a part of the planned path. Here are some results:

![](/images/portfolio-astar/astar-ikonline.png)