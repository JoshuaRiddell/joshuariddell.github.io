---
layout: post
title:  "Vertigo3 Glider"

start_date: 2019-11-15
date:   2020-09-20 13:14:53 +1000

permalink: /projects/megabot-madball-challenge/
subtitle: An agile, towable, underwater camera used in marine research and surveying.
cover-image: /assets/vertigo/glider.jpg

published: false
---

## [Aim](#aim)  {#aim}

This was a project with CSIRO. 

My aim for this project was to increase my robot simulation abilities in the Gazebo simulator, and improve my skills in using the ROS tf2 transformation library by using it for robot localisation.

## [Hardware](#hardware)  {#hardware}

The holonomic base (steppers and laser-cut acrylic) was built by my teammate, Shane Gingell. The base consumed x,y,yaw velocity commands and emitted the current pose of the robot based on wheel odometry. I handled the lifting mechanism, and all other software modules including ball detection, line detection, long-term localisation, motion planning and behvaioural state machine.

The robot uses a Raspberry Pi 4 for all high-level processing. Motor velocity control and wheel odometry is done using an STM32 microcontroller. Basic control of lifting sensors and actuators is done using an ATMEGA328 on an Arduino mini board. Both of these boards are interfaced to the Raspberry Pi using rosserial, which uses UART as the transport.

![raw-image](/assets/megabot/system_overview.png)

## [Simulation](#simulation)  {#simulation}

The robot was simulated using Gazebo simulator with ROS integration. The purpose of the simulator was to develop computer vision algorithms, code for localisation, and code for motion control, without the need for robot hardware. This was useful since the robot was not built unit about 8 out of 10 months into the project.

![raw-image](/assets/megabot/gazebo_sim.png)

## [Localisation](#localisation)  {#localisation}

Localisation is done using computer vision an the ROS tf2 library. An image processing algorithm locates the tip of white lines located on the playing field. A correction transform can then be applied to adjust for odometry drift by knowing the measured and expected position of the line tip. The image below shows an example of this correction transform.

![raw-image](/assets/megabot/correction_transform.png)

## [Motion Planning](#motion-planning)  {#motion-planning}

Motion planning is done using a simple velocity-based controller. The velocity of the robot is controlled based on the 

<!-- Example of the robot moving to positions in a square -->
<iframe width="100%" height="416" src="https://www.youtube.com/embed/jGWijMOJWrM" frameborder="0" allowfullscreen></iframe>

## [Behavioural State Machine](#state-machine) {#state-machine}

Smach is use for behaviour sequencing. This is ROS-integrated state machine library with support for calling standard actions and services. Using this state machine library allows complex behaviours to be encoded in a simple to understand and easy to visualise manner. Smach also allows real-time viewing of the current robot state which imprvoes debugging ability.

<!-- Image of smach state machine -->



