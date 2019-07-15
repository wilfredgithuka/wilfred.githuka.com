---
title: "Preparing_RaspberryPi_For_WiringPi"
date: 2018-06-06T18:39:51Z
subtitle: "Installing WiringPi on The RaspberryPi"
tags: [RaspberryPi, C++, Make, Cmake, Wiringpi]
draft: true
---
The RaspberryPi has been around in the recent years and has become the go-to device to do open computing with a robust hardware. My RaspberryPi 2 is the Model B version 1.1 and I am using it to control my Self Driving RC Car. You can read more about this project here.

I was working with Python before but it since a high level language, I needed more access to the hardware and more performance. So I have decided to code using C++ on the same Archlinux OS.

The following steps assume that you have a newly installe Archlinux OS and you are now waiting to get started developing with C++ and WiringPi.

##  WiringPi
WiringPi is a PIN based GPIO library wirtten in C for the RaspberyPi devices. According to the developer's website its intended for experienced C++ users but I still think even newbies can still find their way when using it. Its application is fairly straight-foward. Arduino's wiring users will find the syntax similar.

#### Setting Up The Environment
The first thing is to make sure that you have the latest system:
```console
sudo pacman -Syu
```
#### Install the Developer tools
```console
sudo pacman -S gcc cmake make git
```
#### Install an Editor or IDE
```console
sudo pacman -S emacs nano
```
#### Install WiringPi
```console
sudo pacman -S wiringpi
```

## Testing WiringPi Installation
We need to verify that the installation was sucessful. Run the follwing code to scan all your GPIO ports and it will present you with a nice picture of the mappings.

```console
gpio readall
```
Connect an LED with a 300Ohm Resistor in series to GND Pin(Pin 6) and Pin 0(Pin 11). Once you have this connection, run the following code to turn the LED ON/OFF

```console
gpio mode 0 out
gpio write 0 1
gpio write 0 0
```

## References
* [Globlib4u]{https://globlib4u.wordpress.com/2013/06/09/raspberry-pi-arch-linux-arm-tutorial}
