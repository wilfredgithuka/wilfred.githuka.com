---
title: "SMPS Detailed Principle of Operation"
date: 2019-09-07T13:09:17Z
draft: false
---
This is a detailed explanation of the inner workings of a Switched Mode Power Supply.
I have written a more simpler version which I recommend you read before coming to this one.

### SMPS Specs

* Input Voltage: 240V AC
* Output Voltage: +12VDC, -12VDC, +5VDC(Regulated),GND 0V

### Components

* 1x Main 240V Fuse
* 1x NTC x1
* 4x Rectification Diodes
* 2x 10 Micorfarad 240V Smoothening Electrolyctic Capacitors
* 1x 1mH Inductor
* FDM311 Green Mode FairChild Power Switch
* 2X 120KOhm Resistors (Snapper)
* 1x 1kV Capacitor(Snapper)

### Input

The SMPS has an input of 240VAC which passes through a fuse and an NTC.

### Rectification

For rectification, it uses 4 Diodes and the rectification has an output of 320V DC. In theory
we can calcuate the expected voltage at the output of the rectification. In Kenya our input voltage
is 240VAC, but it flactuates up to 10%. 240Vx1.414 This can make the rectification voltage rise up to 380V DC.
Rectification increaes voltage so be safe around such high DC voltages. The rectification stage also has 2x10microfarad
220V capacitors and a 1mH inductor coil for smmothening the output.

### FPS Chip

The Chip here is a FSDM311 300V rated chip that does most of the control work in this circuit. In other boards, its replaced by
a discrete transistor. The [datasheet](ttps://www.onsemi.com/pub/Collateral/FSDM311A-D.pdf) is available. The Chip has the following
pin connections, which will be useful in the explanation for this post.

* PIN1 - Ground
* PIN2 - VCC
* PIN3 - Vfb
* PIN4 - NC
* PIN5 - Vstr
* PIN6 - Drain
* PIN7 - Drain
* PIN8 - Drain

The Pin5 Vstr(Startup) is connected to the 320V DC from the rectification stage accross a 10Kohm resistor. At start-up, the  internal switch 
supplies internal bias and charges an external storage capacitor(10 microfarad 50V) placed between the Vcc Pin 2 and ground Pin 1. 
Once the VCC reaches 9V, the internal switch stops charging  the capacitor. To run, the chip uses the aux winding to produce power for the
capacitor. The 10Kohm resistor is used momentarily just for startup since if the 300V was used for a long time it would disspate alot of power.
The chip used the aux winding and the diode to produce 12VDC for running.

The voltage drop at the startup resistor is normally 0.24V with a current of 0.024mA. The voltage is low since it flows here momentarily, for
turning on the chip then drops to minimum. The voltage drop accross PIN 3 for Vfb fedback voltage is 0.68V. Voltage drop accross PIN2 VCC is 0.18V.
But Voltage drop accross PIN2 and ground is 13.17V. Once the Vcc reaches 9V the internal switch stops charging the capacitor.

### Snapper Network

There is a snapper network in the primary consisting of an  [FR107 Diode](https://www.diodes.com/assets/Datasheets/products_inactive_data/ds26001.pdf), 1nFarad 1kV Capacitors, 2 X 120Kohm resistors and 1x 500ohm Resistor.
The FR107/FR106 Diode are known as Fast Recovery Rectifier diodes.
They are put here to protect the chip when it turns OFF since it can generate a large voltage peak which shall be clamped by the network. 
The diode shall rectify the impulse into the capacitor which shall later dispate it into the resistors.

Note that since the 2 resistors are connected accross the HVDC Line, there shall be a voltage drop of 100V DC and a current drop of 0.38A

At the snapper network region, the current shall be 100V/120kOhm to get 0.833A. Power can be calcuated by 100X0.000833A = 0.0833Wx2 = 0.166W rating for
the resistors.
