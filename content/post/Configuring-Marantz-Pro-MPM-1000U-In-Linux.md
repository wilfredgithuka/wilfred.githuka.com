---
title: "Configuring Marantz Pro MPM 1000U in Linux"
date: 2017-12-12T10:52:04+03:00
subtitle: "Recording audio off the Marantz Pro 1000U from terminal"
tags: [marantz, audio, audacity, arecord, alsa]
---
![marantz](/img/marantz.jpg)
The Marantz Pro MPM-1000U is a USB condenser mic for DAW recording or podcasting. It comes in as an entry level mic.It comes with a USB connection which was one of the feature that I wanted. This mic is designed to work on any PC with a
descent USB interface and a software like Audacity. 

While thats good, I wanted to try out recording on termial and this is how far I have come in doing so. Recording audio on terminal offers flexibility and control which might be tough on GUI. On the other hand, its more complicated but with time, you will get used to it.On Linux, recoring with USB mic is best done under ALSA. I am using Archlinux for this expreriment. One of the reasons why am using terminal is for automation. I would like to incorporate bash scripts and python to automate sermon recording at our church.

## Connection

Connect your USB mic and run the following command to check if its detected.

* cat /proc/bus/usb/devices

To check that ALSA detects your mic, run

* cat /proc/asound/cards

## Configuring

Adjust the volume levels of the mic. The number 2 represents what the system has assigned my mic. This will varry accross different machines, so take note from the above commands the number of your mic. This command with open a window form where settings can be made.

* alsamixer -c 2

## Recording

To record a 20 second clip, run this command. Explanation on what happens re there below:

* arecord -f cd -D plughw:2,0 -d 20 /home/wilfred/test.wav
