---
layout: post
title:  "Maze Solving Robot"

start_date: 2017-7-24
date:   2017-11-10 13:14:53 +1000

permalink: /projects/maze-solving-robot/
subtitle: A group project which involved moving a marked puck through a maze using a robotic arm and computer vision.
cover-image: /assets/maze-solving-robot/thumbnail.png

published: true
---

## [Aim](#aim)  {#aim}

This project was for the UQ course METR4202 - Robotics and Automation. The aims of this course are to develop students' skills in classical computer vision techniques, kinematics techniques, and combining these concepts together into a fucntioning robot.

The purpose of the robot was to navigate a "puck" (Australian 20 cent coin) through a varying maze constructed of hard foam blocks to a goal circle - a valid path is shown in the image below. Extra points could be obtained by rotating a black marking on the coin to the same orientation as the goal destination. Extra points were also awarded for precise positioning of the puck on the goal circle.

<p align="center">
	<img width="70%" src="/assets/maze-solving-robot/maze_setup.jpg">
</p>


## [Hardware](#hardware)  {#hardware}

The high-level design constraints were:

* 30x40cm (A3 sized) work area
* 4 actuators
* x-y planar manipulation ability
* coin rotation control
* price
* construction simplicity

Based on these design constraints the following arm was constructed of aluminium square cross-section, MDF and pine wood. The link lengths were the minimum length needed to practically cover the work area. Two revolute links perpendicular to the plane of operation provided the x-y movement, a parallel revolute link allowed the end effector to be raised and lowered, and a final actuator aligned axially on the end effector allowed for coin rotation.

![raw-image](/assets/maze-solving-robot/base.jpg){:width="50%"}![raw-image](/assets/maze-solving-robot/workable_area.jpg){:width="50%"}

## [Software](#Software)  {#software}

A top-down camera mount could not be used (due to challenge imposed restrictions). To overcome this issue, a homography was used to transform the image into a top-down view. Then a combination of HSV colour segmentation and Hough line detection were used to segment the image. An example homographied image is shown below.

![raw-image](/assets/maze-solving-robot/homography.png)

The bolbs in the segmented image were then classified into puck position, goal position and the different block shapes and heights. This allowed the construction of a 2D map of the playing field. The A* algorithm was then used to search for a path between the puck and goal based on a cartesian heuristic. An example 2D binary map is shown below.

![raw-image](/assets/maze-solving-robot/path_panning.png)

## [Results](#Results)  {#results}

The project scored 90% in the demo (+10% grade bonus since we were the only team to demo early). The following is a video of testing phase of the arm. (in the final demo the goal was secured to the playing surface).

<iframe width="100%" height="416" src="https://www.youtube.com/embed/Vds7TOmA23E?t=36" frameborder="0" allowfullscreen></iframe>
