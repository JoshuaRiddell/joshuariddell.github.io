---
layout: post
title:  "MicroPython Quadruped"

start_date: 2018-11-1
date:   2019-1-28 13:14:53 +1000

permalink: /projects/micropython-quadruped/
subtitle: A small project developing a dynamic gait model for a low cost quadruped robot.
cover-image: /assets/micropython-quadruped/thumbnail.png

published: true
---

## [Acknowledgements](#acknowledgements)  {#acknowledgements}

Thank you to Shane Gingell from [Out of The BOTS](https://www.facebook.com/outofthebots/) for providing the robot control board and hardware.

## [External Links](#external)  {#external}

* [Micropython Library](https://github.com/joshuariddell/botslib)
* [C Library](https://github.com/JoshuaRiddell/MicroPython_ESP32_psRAM_LoBo_BOTS) (reimplementation of some Micropython functions in C for extra speed)

## [Aim](#aim)  {#aim}

My personal aim for this project was to gain some experience developing simple kinematic and gait models for legged robots. The main challenge of this project was to make a gait model which can take dynamic input from a gamepad controller. To do this I planned on levereging the MicroPython web framework to handle high-level web interfacing, and using low-level C-libraries for fast execution of kinematic code.

## [Hardware](#hardware)  {#hardware}

The hardware (electrical and mechanical) were already constructed by Shane Gingell for his hobby robotics startup business. I took on the robot to make some core hardware libraries which would hopefully help people who bought the board get started with using it.

The hardware is shown below. It consists of a control board equipped with ESP32, LCD and 16 channel PWM driver. The actuator hardware is 9g hobby servos. Each leg has 3DOF.

<p align="center">
	<img width="70%" src="/assets/micropython-quadruped/main.jpg">
</p>

## [Kinematic Model](#Kinematic Model)  {#kinematics}

The kinematic model consists of two main components, the static inverse kinematic which implements body roll, pitch and yaw movements; and the gait model which determines the stepping pattern.

### [Static Model](#Static Model)  {#static}

Using my model, the quadruped's position can be fully defined using:

* `x,y,z` body translations,
* `r,p,y` body rotations,
* `[[x,y,z], [x,y,z], [x,y,z], [x,y,z]]` array of leg tip coordinates defining stance.

When the body translations and rotations are altered, the body moves and the stance remains unchanged. When the leg coordinates are altered, the legs move and the body position remains unchanged (within reason). Using this setup, the position of the robot in space can be manipulated by movement of the legs directly, and during walking activities the body can be leaned using the body translation and rotation parameters.

An example of the use of body coordinates to translate and rotate the body is shown in the video below. (The front left leg lifts since the gait is active but disregard that for now).

<iframe width="100%" height="416" src="https://www.youtube.com/embed/jGWijMOJWrM" frameborder="0" allowfullscreen></iframe>

### [Gait Model](#Gait Model)  {#gait}

The gait model adds a "base stance" parameter to the kinematics model. This consists of coordinates in the form: `[[x,y,z], [x,y,z], [x,y,z], [x,y,z]]`. The base stance stores the desired leg positions at rest.

A crawl gait will be implemented because it looks the coolest. The general sequence of movements for my gait implementation is:

```
while true
    calculate_leg_distances()
    for leg in legs
        if leg.distance_to_base_stance > STEP_THRESHOLD
            lean_body()
            step_leg()
```
`calculate_leg_distances()` calculates the difference between each leg position and the desired base stance. \\
`lean_body()` leans the body such that the centre of mass of the quadruped is inside the base of support for the three legs which are not currently stepping. \\
`step_leg()` lifts the stepping leg up and moves it back to the base stance position.

Although this pseudocode shows the general logic, it has some issues. For example the lean_body and step_leg routines will take in the order of seconds to execute since they should be smooth motions. One way to rectify this is to make an intermediate motion planning layer between the kinematic model and leg hardware. Another way to implement this is to make the lean_body and step_leg routines non-blocking such that they can be periodically called to update the leg position. The non-blocking method was chosen because of its simplicity.

The gait model is programmed as a state machine with the following states:

1. IDLE
2. LEANING
3. STEPPING

The `IDLE` state maintains the body lean at `(0,0)` (which resets the body after a stepping event). The leg distance calculation and threshold checking is performed in this state. When a leg is over the stepping threshold, the leg is chosen as the "stepping leg", and the state is transitioned to the `LEANING` state. The `LEANING` state slowly moves the body over the centre of support of the three legs left excluding the "stepping leg". When the centre of gravity of the body is inside the triangle of support made by the three non-stepping legs, the state is transitioned to the `STEPPING` state. The stepping state lifts the "stepping leg" and places it back down at the "base stance" position. Once the step has been executed, the state transitions back to the `IDLE` state.

A demo of the stepping state machine is shown in the video below.

<iframe width="100%" height="416" src="https://www.youtube.com/embed/r83PZAL-xRE" frameborder="0" allowfullscreen></iframe>

## [Web GUI](#Web GUI)  {#web_gui}

A web GUI is used as the main interface to the robot. Through a MicroPython websockets interface, the robot gait can be fully configured. The websocket connection is also used to stream controller commands. This allows me to leverage the HTML5 GamePad library and so not have to write complex gamepad drivers, but of course has the disadvantage that the robot cannot be directly controlled without a mobile phone/computer middle layer. The simple GUI is shown below.

<p align="center">
	<img width="60%" src="/assets/micropython-quadruped/web_gui.png">
</p>

## [Walking Demo](#Walking Demo)  {#walking}

Shown below is a walking demo. The robot is being controlled by an XBox controller via a websocket connection. This demo shows the gait model is quite responsive and can be used for relatively precise controlling of the robot.

<iframe width="100%" height="416" src="https://www.youtube.com/embed/W5jvR6bzVPM" frameborder="0" allowfullscreen></iframe>

## [Future Improvements](#Future Improvements)  {#improvements}

One large improvement could be made by either throttling the human input dynamically based on the leg positions, or switching to a faster gait type based on how much control input is used. Dynamic switching of gaits would likely benefit from implementation of an intermediate motion planning layer which handles smooth transitioning between the gaits at speed. 