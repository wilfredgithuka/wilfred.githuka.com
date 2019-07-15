---
title: "My Encounter With The STC Microcontrollers"
date: 2018-01-26T18:18:35+03:00
subtitle: "The STC15xx series is a low power stable microcontroller"
tags: [stc, microcontroller, 8051, stcmcu]
---
![image](/img/avic-kist/stc.JPG)

The first time I held an STC microcontroller was today morning when we were
preparing the lab ahead of the class experiment for tomorrow. I decided to assemble my own board from the components given. The boards were packed tightly in bulk so it was quite a task to set them up. The boards which I later came to learn were designed by one of the Chinese's lecturers students back in China. The size of the boards are twice the size of a Raspberry Pi and the thickness is almost 2mm.

The 8051 Microcontroller was designed in 1980’s by Intel. Its foundation was on Harvard Architecture and was developed principally for bringing into play in Embedded Systems. At first it was created by means of NMOS technology but as NMOS technology needs more power to function therefore Intel re-intended Microcontroller 8051 employing CMOS technology and a new edition came into existence with a letter ‘C’ in the title name, for illustration: 80C51. These most modern Microcontrollers need fewer amount of power to function in comparison to their forerunners.

There are two buses in 8051 Microcontroller one for program and other for data. As a result, it has two storage rooms for both program and data of 64K by 8 size. The microcontroller comprise of 8 bit accumulator & 8 bit processing unit. It also consists of 8 bit B register as majorly functioning blocks and 8051 microcontroller programming is done with embedded C language using Keil software. It also has a number of other 8 bit and 16 bit registers.

### Assembly
One thing to note is that for the STC, its the Chip that you buy then design a board for it. We get these boards from China but I would like to design my very own board then chip-it. The task is to assemble SMD components onto the board, a task thats not easy due to the small parts. Next is to connect it to the computer via USB and load a program into it. The teacher's laptop, running Windows had a Chinese-made program that is used to program the board as I soon found out. But being a linux guy, I googled something and found lots of Python based alternatives that could communicate with the board over the USB interface. I came accross one called [stcgal](https://github.com/grigorig/stcgal) which worked well. The installation procedures are quite simple and well documented.

### stcgal
stcgal requires Python 3.2 (or later) and pySerial. USB support is optional and requires pyusb 1.0.0b2 or later. You can run stcgal directly with the included stcgal.py script. The recommended method for permanent installation is to use Python's setuptools. Run ./setup.py build to build and sudo ./setup.py install to install stcgal. A permanent installation provides the stcgal command. Be sure to have setuptools and tqdm installed as dependancies for stcgal. Connect the board and Linux will detect it then run stcgal for it to dump the chips details. This is what I got:

* Waiting for MCU, please cycle power: done
* Protocol detected: stc15
* Target model:
  * Name: STC15F2K60S2
  * Magic: F408
  * Code flash: 60.0 KB
  * EEPROM flash: 1.0 KB
* Target frequency: 11.069 MHz
* Target BSL version: 7.2.5S
* Target wakeup frequency: 35.900 KHz
* Target options:
  * reset_pin_enabled=False
  * clock_source=internal
  * clock_gain=high
  * watchdog_por_enabled=False
  * watchdog_stop_idle=True
  * watchdog_prescale=256
  * low_voltage_reset=True
  * low_voltage_threshold=3
  * eeprom_lvd_inhibit=True
  * eeprom_erase_enabled=False
  * bsl_pindetect_enabled=False
  * por_reset_delay=long
  * rstout_por_state=high
  * uart2_passthrough=False
  * uart2_pin_mode=normal
  * cpu_core_voltage=unknown
* Disconnected!

Am yet to decipher much of the information above. With time however I will make
up followup posts explaining in detail what each means. stcgal supports Intel HEX encoded files as well as binary files. Intel HEX is autodetected by file extension (.hex, .ihx or .ihex).

### STC15F2K60S2

The STC15F2K60S2 series MCU is a single chip microcontroller based on the 8051 CPU produced by STC MCU Limited. This new generation is faster, more stable and
has low power consumption. Its about 8-12x faster than the original 8051(Am yet to test this allegation). Further reading showed that it has 2kB of SRAM and two fast asynchronus serial ports: UART 1 and 2.

### Programming

To program the STC15F2K60S2 chip you need to write your program in Embeeded C
then convert it in .hex format which is uploaded into the chip via the boards USB interface. On Windows, the software is called Keli which is an IDE. In Linux am yet to write my own code so I cant say much about it, but am sure there are lots of examples out there.

The board is currently working as my desktop digital clock as I figure out how to program it. This digital clock is the teacher's program running in there, I cant wait to write mine.

You can check out my [github repo](https://github.com/wilfredgithuka/keil-c-development-work) for updates and code.

### References

* https://www.elprocus.com

This post was written in Spacemacs :-) over a cup of uji.
