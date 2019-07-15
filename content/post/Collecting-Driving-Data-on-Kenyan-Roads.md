---
title: "Collecting Driving Data On Kenyan Roads"
date: 2017-09-22T23:58:07+03:00
subtitle: "How to collect your data safely and on budget"
tags: [self-driving-car, autonomous-vehicle, udacity, dashcam]
---
![Final Image](/img/udacity/nairobimg4.jpg)

Ever since I dipped my mind into the autonomous vehicles world, I have been noting carefully road transport in a whole new dimension. I now see data and need lots of it. Training a CNN needs alot of data and even when I was working on the Lane Detection Algo project, I used data that was provided by (Udacity)[udacity.com]. But now I deceided to put the same algo on local roads here in Kenya. I can carry my laptop but that will be cumbersome and even risky. So I decided to use my smartphone's video cpability to record  a driver driving during my commute to work or errands.

Before I go further, I would like to insist on safety. When you are collecting your data, always keep your eyes on the road and be safe. This is experiemental technology which needs alot of tests before its safe and legal. If you are on the passenger's side, don't distract the driver. Talk to the driver before installing anything and install it when the car is stationery so that when the driver is driving, its not distracting him. Safety First.

I built a small rig made from the selfie stick which has an excellet phone gripper which I attatched to a tin lid for the base. The unit sits nicely on the dashboard of any car which is smooth, but sometimes needs to be held down by masking tape on rough roads. Using this rig I have collected upto 40kms or road data in video format for my studies and research.

![Final Image](/img/udacity/phone-mount.jpg)
Here is my rig - The wilrIG

## Tools
The following are what you will need to start data collection. This tutorial assumes that you have Linux OS installed on your machine.

* Rig or dashcam
* FFmpeg - Powerful video tool
* ImageMagic - Powerful comand line image editor
* Time, patience and humility - Peeps gonna ask you what you are doing

## Pipeline (Workflow)
This is my workflow to manage the data connected. I am constantly updating it and making it more efficient.

* Record data in video format without audio. Turn OFF audio recording in phone or webcam settings. Audio increases file size significantly so I dont need it. Put phone in Flight Mode during data collection to stop disruptions when the phone is called or notifications. Be sure to have enough memory card space. 
* Transfer video to computer and rename appropiately
* Fire up FFmpeg and run these commands to cut the parts of the video you want, reduce resolution of video down to 640:360 and extract images from video 
* Scale down the resolution

```bash
ffmpeg -i inputvideo.mp4 -vf scale=640:480 outputvideo.mp4
```
* Get the wanted parts of the video 

```bash 
ffmpeg -i inputvideo.mp4 -ss 00:04:24 -to 00:06:40 -c copy outputvideo.mp4
```

* Extract Images(s) from video

```bash 
ffmpeg -i inputvideo.mp4 -ss 00:00:13.000 -vframes 1 ImageOutput.jpg
```
* Extract Image from video with specific time/intervals

```bash 
ffmpeg -i inputvideo.mp4 -vf fps=1/15 ImageOutput.jpg -hide_banner
```
* The video you have and images are ready for testing. Create appropriate folders to kep your work neat. Am working on a bash script to simply all this, so stay tuned.

Header Image/MagicalKenya.com

