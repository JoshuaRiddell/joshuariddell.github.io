---
layout: post
title:  "Self Driving Model Car"

start_date: 2016-03-21
date:   2016-07-20 13:14:53 +1000

permalink: /projects/self-driving-model-car/
subtitle: A self driving car following a coloured track using classical computer vision.
cover-image: /assets/self-driving-model-car/thumbnail.jpg

ongoing: false
published: true
---

With thanks to [Lachlan Robinson](https://www.linkedin.com/in/lachlan-robinson) for the fantastic thumbnail image.

![car](/assets/self-driving-model-car/car.jpg)

## Quick Links

#### Internal
* **[Computer Vision](#cv)**
* **[Hardware](#hardware)**
* **[Videos](#videos)**
* **[Future Plans](#future)**

#### External
* [Github Codebase](https://github.com/joshuariddell/self-driving-model-car)

* [QUT Robotics Article](https://qutrobotics.club/2016/07/19/how-to-make-an-autonomous-vehicle-the-2016-droid-racing-challenge/)
* [QUT Promo Video](https://www.youtube.com/watch?v=523I053X8xI)

## Overview

The robotics club at Queensland Univeristy of Technology ran a competition aiming to produce fully autonomous racing cars which stay inbetween blue and yellow coloured lines in relatively challenging lighting conditions. The competition was very open, with the only constraints being size restrictions and no external sensors (such as GPS). The use of computer vision was encouraged.

I lead the team entry from UQ. Our car used colour thresholding and binary image morphological operation to find the position of the line. It then uses a simple proportional control algorithm to follow the line. A PID would've been too tempermental at this early stage in development. We came second in the competition, with time constraints due to the competition being held around exam time being the main challenge. The competition overall was a very good experience and I will definitely be competing next year.

## [Computer Vision](#cv) {#cv}

The computer vision side of the project was quite simple. The following steps were performed:

* A frame was taken from the camera;
* A box filter was applied (blurring to smooth out the colours);
* The colour space was converted to HSV (allows for colour thresholding);
* The image was thresholded based on stored colour parameters.

The video below shows these steps in action.

<iframe width="100%" height="416" src="https://www.youtube.com/embed/sgeT_iDKmbI" frameborder="0" allowfullscreen></iframe>

## [Hardware](#hardware) {#hardware}

# Integration

The diagram below shows an overview of how the car's hardware communicates with I/O devices. The components are described further in the following sections.

![hardware-topology](/assets/self-driving-model-car/diagram.png)

# Sensors

Two sensors were set up on the car, a webcam and ultrasonic distance sensor. The webcam was used for detecting the track as seen in [Computer Vision Section](#cv), and the purpose of the ultrasonic sensor was to detect obstacles and other cars on the track.

# Computing

A Raspberry Pi is used for high level processing on the webcam data. The Arduino is used for interfacing with low level electronics which require accurate timing or an analogue input. The RPi has trouble with PWM on multiple pins it's also trying to run an operating system at the same time. Currently, all logical operations to do with navigation are performed on the RPi.

# Car Components

The car runs of a 2/3 cell series lipo battery (7.4-11.1V resting voltage). It can pull ~110A from the battery, giving ~1.3kW of power in a car which weighs ~5kg. The car power system was originally built to be a high powered racing model so it can reach speeds of ~95km/h when under human control. The aim is for the weakest link to be the comptuer vision algorithm, allowing for better research in that area.

## [Videos](#videos) {#videos}

In the below video, the car is driving full autonomously the evening before the competition.
<iframe width="100%" height="416" src="https://www.youtube.com/embed/DavB7bqimz4" frameborder="0" allowfullscreen></iframe>

## [Future Plans](#future) {#future}

The competition is likely to run next year in a similar format, so I will be keeping the car and adding to it. I expect that the entry will be much stronger next year.

The planned features are:

* Reliable video/data streaming to a mobile device to improve debugging ability
* Use of machine learning (likely convolutional neural networks) to improve the robustness of the computer vision algorithm