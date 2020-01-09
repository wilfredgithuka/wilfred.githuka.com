---
title: "No Screen. Access Rpi Model A via Serial Port"
date: 2019-10-12T12:33:27Z
draft: false
---
The Raspberry Pi Model A Revision 2.0 is a really classic device. On of the early
devices to be made in early 2011 and its still working upto this date.

I have been having it for a while  but these days I normally use it for learning
purposes, mostly a general purpose computer.

This manual is for those who dont have a HDMI or RCA cable for setup. I will be
connecting it up on a serial port which is quite handy.

## Requirements

* Raspberry Pi Device
* USB-Serial Cable with 3.3V RS-232 Level Converter

## Console Seial Parameters

The following parameters are needed to connect to the Raspberry Pi console, and apply on both Linux and Windows.

* Speed (baud rate): 115200
* Bits: 8
* Parity: None
* Stop Bits: 1
* Flow Control: None

## Raspberry Pi serial connection

Connect the USB-Serial cable as per the image below.

![image](https://elinux.org/images/thumb/1/13/Adafruit-connection.jpg/300px-Adafruit-connection.jpg)

## Linux PC Setup

On the pc check whether the USB-Serial Device is being identified:

```
ls -l /dev/ttyUSB0
```
If its listed, thats good, now proceed to launch gnuscreen. If its not 
installed, please install it.

```
screen /dev/ttyUSB0 115200
```

Power on the Raspberry Pi and the information should be available on the
pc terminal screen.

## References

* [RPi Serial Connection](https://elinux.org/RPi_Serial_Connection#Connection_to_a_PC)

