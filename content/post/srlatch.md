---
title: "The SR Latch Explained"
date: 2019-07-25T05:39:48Z
draft: true
---
The SR Latch also known as Set Reset Latch is the basic latches and a stepping
stone to understand most of the other latches. It is from the SR Latch that
am going to describe the other 4 Latches and Flip flops, namely:

* SR Latch
* D Latch
* D Flipflop
* SR Flipflop
* JK Flipflop

### Difference between a Flipflop and a Latch

In the simplest terms, in a latch the output will change whenever the input changes
but in a flipflop, the output shall only change when there is a clock pulse, therefore
a flipflop always has a clock signal.

### Components

To build an SR Latch we shall need the following:

* 74LS32 Quad 2 Input OR Gate
* 74LS02 Quad 2 Input NOR Gate
* 1 LED
* Breadboard & Wires
* 330 Ohms Resistors
* Power Source 5V (Phone Charger)

### Working Principle

To be able to explain the working principle of the SR Lath well, we have to know that
it works in 5 unique states to make the Set and Reset work well. In the diagram above I 
have indicated the unique states from 1 to 5. Refere to the truth table for any clarification.

* State1: In a NOR gate, when both inputes are 0 the result is a 1. Therefore the top NOR gate
turns ON which causes a 1 to be sent to the second NOR gates' input signal. This then causes it
to have a 1 and 0 at its input which results in a 0 at the output.
* State2: We the  apply a 1 signal at the first NOR gate. This has no effect since in a NOR gates
a 1 and 0 will result in a 0 output.
* State3: In this state, as per the diagram, the Latch is not changing since its still a 1 and 0.
* State4: We then apply a 1 and 1 at the first NOR gate. The result according to the truth table is
a zero output. However, the second 1 input of the first NOR gate is tied to the second NOR gate's output.
This causes a 1 output at the second NOR gate. The output of the two NOR gates appear to be in opposite.
* State5: We now rename the top input as S for Set and the second one as R for Reset. It can also
be notted that if you want to set the Q output then you have to put a 1 at the S input.

### Logic

To understand the SR Latch well, you have to build the circuit as per the diagram.




