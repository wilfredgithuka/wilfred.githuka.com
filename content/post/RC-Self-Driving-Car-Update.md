---
title: "RC Self Driving Car Update"
date: 2017-08-03T08:49:53+03:00
subtitle: "An update on my progress in buiding a small Self Driving Car"
tags: [RCSDC, Udacity, Python, RaspberryPi, Self-driving, Autonomy]
---

Of late I have been busy making the car since my last update. If you do not undertsand what this project is aout, please check the last update and check out my medium page where I give regular updates. Its so easy to blog on medium.

In summary the following have happened since April

* Learned alot about Self Driving Cars from Udacity
* Bricked a Raspberry Pi Model 3
* Bought and destroyed an RC Car
* Coded alot in Python
* Eploded a LiPo battery

![Example image](/img/lifelog/June-16-2017-23_50_08.JPG)
One of my main challenges with the RC Self Driving car was power. My initial buid was hardly moving. Infact it was creeping. The batteries couldn't produce enoug power to move it faster.I acicentaly broke the front axle of the car. This is the part used to turn the wheels. This made me put the car aside and concentrate on the software hoping to figue out a way to solve the axle issue in the process.

The solution was painful, after opeing up the car's internals the damage seemed irreparable and given that these cars are Chinese made, there are no spareparts.I resulted to buying a new smaller car which I also hoped would be able to solve the power option. After removing the outer shell, I mounted the pi and breadboard, did the wiring and plugged in the power. Power source is provided by my bench power suppy at 6VDC 1000mA. The cars wheels rotate fast when on a bridge but when I placed it on a surface while still tethered on the power supply, it still crept.

I soon realised afther running some tests the rear motor was not powerful enough to move the car despite an increase in voltage to 7V. I finally repaired my old car and used super glue to fix the axle problem. Mounted the circutry and added more juice (power) to the rear motor. This juice is a 7V LiPO battery pack that will drive the rear and front wheels steering servo motor. For the raspberry pi I got a 6000mAh China made power bank and I used SSH to connect to it. The car is now independent and I have got enough power for the motors. LiPo batteries are good but need to be well taken care off. The power bank provides the 5V 800mA min current to switch on the RaspberryPi. Essentially the pi controls the car via the GPIO pins with the help of a L293D motor driver.

The car is now running weel and am poishing the code to basic movement. Whats left is now the software which will define motion, path planning and self driving movements.

