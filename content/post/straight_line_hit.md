---
title:       "Path Planning in C++ Part 2"
subtitle:    "Second Part For Developing a path planning algorithim to drive a car"
description: "In part 1 I managed to move the car but in just straight line. In this second part I try to make the vehicle stick to the lane."
date:        2019-01-16
author:      "Wilfred Githuka"
image:       "/img/Car_Move_But_Hits_Other_Vehicles.png"
tags:        ["autonomous-vehicle", "udacity"]
categories:  ["Autonomous-Vehicle" ]
---

I managed to solve the driving-in-a straight line by calculating the trajectory of the vehicle instead of directly
feeding the trajectory as I had done earler. This can be seen in the image below. 

![image02](/img/Car_Move_But_Hits_Other_Vehicles.png)

But now I have developed another problem such that my vehicle is hitting other cars on the same lane. 
I thought I would be able to solve this by reducing the value of dist_inc down to 0.3 from 0.5. 
This worked only on a conditon that the vehicle infront of me was not slowing down. Also my car is 
violating jerk and acceleration laws.

Now how can I slow down once my vehicle sensors tell it that there is another vehicle infront?

Let me see...
