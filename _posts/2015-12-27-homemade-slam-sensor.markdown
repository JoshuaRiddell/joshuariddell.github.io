---
layout: post
title:  "Homemade SLAM Sensor"
start_date: 2015-12-25
date:   2015-12-26 13:14:53 +1000
categories: blog
permalink: /:categories/:title/
subtitle: My first attempt at a basic simultaneous location and mapping robot.

published: true
---
## Quick Links

Lorem ipsum dolor sit amet.

## Aim

The aim of this project was to:

* refine my mechanical design and manufacturing skills;
* gain experience in creating electrical connections over moving parts;
* create a basic SLAM (simultaneous location and mapping) sensor at a low cost;
* design basic location algorithms.

## Hardware Design

# Worm Gear-set

The motor I had handy ran at approximately 11,000RPM@5V (no load). I estimated that approximately 120RPM would be a reasonable speed for the sensor rotor giving a 2Hz full refresh rate. I was not aiming for a high performance sensor and higher speeds would need a well balanced rotor.

![gear-iterations](/assets/slam-sensor/gear-iterations.jpg)