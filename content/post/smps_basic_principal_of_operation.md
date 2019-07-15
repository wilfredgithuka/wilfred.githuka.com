---
title: "SMPS Basic Principle Of Operation"
date: 2019-05-28T08:58:44Z
draft: false
tags: [smps, electronics, soldering]
---
A Switched Mode Power supply is one of the most efficient ways to step down AC to DC which can
be used by domestic appliances like mobile chargers, laptops and pcs. Its an advancement from
liner power supplies and this technology has seen wall chargers get smaller and more efficient.

In the most simple definition, an smps is a type of power supply that uses semi-conductor devices'
switching techniques rather than the standard linear methods to provide a stable reliable and safe 
output voltage.

In a Linear power supply, the transistor is used to control the voltage drop while in the SMPS, 
the transistor is used as a controlled switch.

The cool thing is that unlike linear power suppliers which can only offer step-down voltage regulation,
an smps can offer:

* Step-down (DC-DC Buck)
* Step-up (DC-DC Boost)
* Negation (DC-DC Buck Boost)

An SMPS works in the following sequence:

* 1. Input: 240V AC (Kenya Power Stuff)
* 2. Recification & Filtering
* 3. High Frequency Converter
* 4. Output Recitification & Filtering
* 5. Feedback Section (Control Circuit)
* 6. DC Output

To get an understanding how the SMPS works, lets look at the block diagram below.


![smps-block](/img/smps_block.jpg)

## Stage1: Input & Filtering
#### Input: 240VAC

First an AC (240V) enters the RF Filter Circuit. The function of this is to prevent the power supply from causing
interference on the main wiring.

#### Output: 240VAC

## Stage2: Rectification
#### Input: 240VAC

The following stage contains a full bridge recitifier. A rectifier is a set of components [diodes] which converts Alternating Current(AC)
to Direct Current(DC). However due to the nature of the diodes, the DC component produced here is very uneven. There is a
provision for a large DC electrolyctic filter capacitor [220 uF, 450V] which helps smoothen the DC to be clean. The output of this stage is a
high voltage DC which is very lethal.

#### Output: 300VDC

## Stage3: Transformation
#### Input: 300VDC

The 'cleaned' DC will then be fed into the startup restistors and also to the input of the SMPT(Switched Mode Transformer). Note that
the startup resistors have a high ohmic value which then causes a voltage drop which goes to the Vcc supply of the PWM IC. The Run-DC
circuit consists of a Resistor and a Diode which maintain the power IC stable operation. Once the PWM IC is ON, it shall produce
a signal to the Power FET transistor and produce a change in the magnetic field in the transformer's primary windings. This change in magnetic
field produces a voltage in the secondary windings.
#### Output: ~48VAC

## Stage4: AC Recitification, Filtration & Regulation
#### Input: ~48VAC

Each of the AC Voltages at the output of the secondary windings of the transformer is then recified, filtered and regulated to produce
a 'clean' DC Voltage which is available at the output.

#### Output: ~12VDC

## Stage5: Error Sampling & Detection Circuit
#### Input: ~12VDC

SMPSs have a feature that sets them apart from the Linear type. A feedback loop system. This samples a part of the output and then checks to ensure
that its constant. If the output starts to fall the PWM IC will act to correct this. This feature causes SMPS wall chargers to continue working
even when the mains voltage drops or is unstable.

#### Output: ~12VDC

That is a simlple explanation of how a SMPS works. In the next article, I will walk with [DiodeGoneWild](https://www.youtube.com/watch?v=cX4q0e124C4) 
in one of his videos abou the SMPS which is going to be very deep and super interesting.

Back to work :-)

