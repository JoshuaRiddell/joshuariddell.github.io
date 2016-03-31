---
layout: post
title:  "Model Black Box Retrieval Craft"

start_date: 2015-03-01
date:   2015-06-05 13:14:53 +1000

permalink: /projects/black-box-craft/
subtitle: A basic search and retrival craft made for a first year compulsory course at UQ.
cover-image: /assets/black-box-craft/thumbnail.png

published: true
---

This was my first university course project. I mainly developed my skills in:

* coordinating and leading a group project;
* producing a working prototype to a deadline;
* engineering report writing style.

## Hardware Design  {#hardware-design}

The requirements of the hypothetical tender proposed by the course was:

* have a sustainable design;
* be constructed using basic hand tools;
* fit inside 200&times;200&times;200mm box (150&times;150&times;150mm for bonus);
* comply with $100 budget ($75 for bonus);
* completely autonomous;
* power for 2&times;5 minute deployments;
* weigh less than 0.5kg for bonus.

The team set out to achieve all of these goals including the bonus specifications.

Mockup of the main full design is shown below.

![hull-mockup-1](/assets/black-box-craft/hardware/drive-prototype-1.jpg){:width="33%"}![hull-mockup-2](/assets/black-box-craft/hardware/drive-prototype-2.jpg){:width="33%"}![hull-mockup-3](/assets/black-box-craft/hardware/drive-prototype-3.jpg){:width="33%"}

Two candidate hull designs, using reused materials, were contructed as shown below.

![hull-prototypes](/assets/black-box-craft/hardware/hull-prototypes.jpg)

The water bottle hull had the buoyancy best suited to the mass of the electronics. And so it was chosen.

Below is the product with all electronics mounted. A geared motor with spool was attached to act as the winch.

<p align="center">
	<img width="50%" src="/assets/black-box-craft/hardware/finished.png">
</p>


## Software Design  {#software-design}

The software was originally intended 

```C++

int code_snippet() {
	hello world
}

```