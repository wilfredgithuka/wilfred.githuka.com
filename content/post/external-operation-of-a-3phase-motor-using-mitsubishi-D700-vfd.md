---
title: "External Operation [EXT] of a Mitsubishi D700 VFD to Control a 3phase Motor"
date: 2018-03-01T12:33:40Z
subtitle: "Realise 3 speed operation of a motor using a VFD"
tags: [3phase, motor, frequency, vfd, mitsubishi]
---
![intro-image](/img/avic-kist/motor-vfd.JPG)

External Operation of a 3phase Motor Using Mitsubishi D700 Inverter
The Mitsubishi D700 Inverter is a very handy variable frequency drive for the electrical 
engineer. This model, though discontinued has been used in a variety of 
connections for different types of loads. In today’s experiment, I want to 
show you how to control a small 3phase motor using the D700 to make the motor 
run in 3 different speeds, and change direction. All this control shall be 
done in EXT mode on the variable frequency drive. For those new to the variable frequency drive, you can 
have a look at this [introductory piece on variable frequency drives](https://en.wikipedia.org/wiki/Variable-frequency_drive) them come back here. 
In EXT mode, it simply means that the variable frequency drive is externally controlled via 
some switches.

## Hardware and their States:
* 3phase 415V asynchronous motor, star connected
* Mitsubishi D700 VFD
* Voltmeter and Ammeter(Digital/Analogue)
* AC 415V power source

## Process
* Connect your motor to power source and add the ammeter and voltmeter as per the diagram below. Take care when working with 3phase voltage
* Connect your variable frequency drive as per the diagram below. If you are using another type apart from the D700, please check its manual on how to make the connections.
* Set Pr. 79 ="3" (EXT/PU combined operation model)
* Use the D700’s operation panel to set the correct frequency.
* Switch terminal STF(STR)-SD on to give a start command.
* Now that the EXT PU LEDs are on set the following parameters: 
Pr.79=3; Pr.7=3.0s; Pr.8=3.0s.
* Turn the dial to set the frequency to 30Mhz
* Connect the 0V terminal on SD terminal.
Operation
* The STF, STR are Start Forward and Start Reverse switches
* The RH,RM and RL are Run High, Run Middle and Run Low are speed selection switches
* Since the Inverter has the EXT/PU combined start the motor using the ON/Start button on the Inverter panel.
* The motor will not run at first, but when you toggle RL the motor will start in slow frequency/speed then when you toggle the RM switch it will pick up speed.Finally toggle RH and the motor will run at the maximum speed/frequency setting available. The values of the different speeds depend on what you set in the beginning for the parameter.
* The motor can also change direction by toggling the STF and STR switches respectively. Note that if both switches are ON the motor will not run, instead come to a halt. 

![final-image](/img/avic-kist/vfd.JPG)
## Explanation
PU/EXT mode comes in handy especially when you want to retain control of the variable frequency drive from the front panel and also from other switches which may be in a different location.

That’s all for now, on the next post I will describe how to completely control the variable frequency drive externally without operating the variable frequency drive from the front panel. Later on I will cover about how to control the variable frequency drive from the PLC.
