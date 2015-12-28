---
layout: post
title:  "Homemade SLAM Sensor"

start_date: 2015-12-25
date:   2015-12-28 13:14:53 +1000

permalink: /projects/slam-sensor/
subtitle: My first attempt at a basic simultaneous location and mapping robot.

published: true
---
## Quick Links

* **[Aim](#aim)**

* **[Hardware Design](#hardware-design)**
	* [Worm Gear-set](#worm-gear-set)

## Aim  {#aim}

The aim of this project was to:

* refine my mechanical design and manufacturing skills;
* gain experience in creating electrical connections over moving parts;
* create a basic SLAM (simultaneous location and mapping) sensor at a low cost;
* design basic location algorithms.

## Hardware Design  {#hardware-design}

# Worm Gear-set  {#worm-gear-set}

The motor I had handy ran at approximately 11,000RPM@5V (no load). I estimated that 120RPM would be a reasonable speed for the sensor rotor giving a 2Hz full refresh rate. I was not aiming for a high performance sensor and higher speeds would need a well balanced rotor. The final gear ratio was limited to 19:1 because of printing resolution, eventually giving a projected speed of 580RPM. Below are the gear iterations which were used to optimise printing performance and gear ratio.

![gear-iterations](/assets/slam-sensor/gear-iterations.jpg)

Next a light box was printed to test the fit the gears. The final tested rotor speed was 320RPM@3.3V which was sufficienty close to the desired speed. One issue was that the gearbox was very loud. This was possibly due to:

* slight printing defects causing vibrations;
* thin case walls amplifying small vibrations.

![gear-iterations](/assets/slam-sensor/first-gearbox-1.jpg){:width="50%"}![gear-iterations](/assets/slam-sensor/first-gearbox-2.jpg){:width="50%"}

These two problems were solved by:

* which were solved by changing from PLA to ABS plastic which can be vapour smoothed;
* using thicker case walls.