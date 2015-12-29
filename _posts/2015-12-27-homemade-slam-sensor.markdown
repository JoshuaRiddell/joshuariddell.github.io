---
layout: post
title:  "Homemade SLAM Sensor"

start_date: 2015-12-25
date:   2015-12-28 13:14:53 +1000

permalink: /projects/slam-sensor/
subtitle: My first attempt at a basic simultaneous location and mapping robot.

ongoing: true
published: true
---
## Quick Links

* **[Aim](#aim)**
* **[Hardware Design](#hardware-design)**
	* 
* rotor


## Aim  {#aim}

The aim of this project was to:

* refine my mechanical design and manufacturing skills;
* gain experience in creating electrical connections over moving parts;
* create a basic SLAM (simultaneous location and mapping) sensor at a low cost;
* design basic location algorithms.

## Hardware Design  {#hardware-design}

### Worm Gear-Set Feasability Testing  {#worm-gear-set}

The motor I had available for use ran with approximately 11,000RPM@5V (no load). I estimated that 120RPM would be a reasonable speed for the sensor rotor giving a 2Hz full refresh rate. I was not aiming for a high performance sensor and the higher the speeds, the better the rotor has to be balanced. The final gear ratio was 19:1 which balanced printing resolution and desired size. This gave a projected speed of 580RPM not accounting for frictional losses. Below are the gear iterations which were used to optimise printing performance and gear ratio.

From left to right: V1, worm pitch is too close to printer resolution; V2, worm pitch too large; V3 balance between print quality and size; V3 accompanying gear; V3.1 gear with bearing attachment.

![gear-iterations](/assets/slam-sensor/gear-iterations.jpg)

The final tested rotor speed was 320RPM@3.3V which was sufficienty close to the desired speed.

![gear-iterations-1](/assets/slam-sensor/first-gearbox-1.jpg){:width="50%"}![gear-iterations-2](/assets/slam-sensor/first-gearbox-2.jpg){:width="50%"}

The main issue during testing was that the gearbox was very loud. This was possibly due to:

* slight printing defects causing vibrations;
* thin case walls amplifying small vibrations.

These two problems were solved by:

* changing printing from PLA to ABS plastic which can be acetone vapour smoothed ([see here](#acetone));
* using thicker case walls.

These tests indicated that the worm gear-set was feasable. The above improvements were implemented into the final design.

### Rotor {#rotor}

The rotor consists of 4 slip rings (+5V, GND, SIG1, SIG2) constructed using ~1.5mm thick copper piping slices. These were inexpensive to produce and provided a good surface for electrical connection. The CAD model and sensor mockup below were an indication of the appearance of the final design.

![design-cad](/assets/slam-sensor/initial-concept-design-cad.png){:width="50%"}![final-design](/assets/slam-sensor/initital-concept-design.jpg){:width="50%"}

### Assembly

The first step in assembly was the rotor, the parts for which are shown below.

From left to right: drive gear (with bearing mount), connector, bearing mount, +5V slip ring, GND slip ring, SIG1 slip ring, SIG2 slip ring, sensor mount, IR sensors.

![rotor-gear-parts](/assets/slam-sensor/final-rotor-assembly.jpg)

During assembly:

![rotor-gear-parts](/assets/slam-sensor/rotor-assembly-1.jpg)

#### Acetone Vapour Smoothing {#acetone}

As part of assembly, the rotor and worm gear were treated with an acetone vapour bath. This temporarily dissolves the outer surface of the parts which merges the layers together. This smooths the outer surface and slightly strengthens the part. The setup consisted of a jar with approximately 10mL of acetone in. The print bed was heated to 90&deg;C and the acetone vapour was allowed to fill the jar. Parts were submerged in the gas for approximately 5 minutes.

![acetone-treating](/assets/slam-sensor/acetone-treating.jpg)

The treated product is shown below.

![treated-rotor-and-worm](/assets/slam-sensor/final-gear-assembly-constructed.jpg)