---
title: "Monostable Mode"
date: 2020-04-03T14:20:31+03:00
draft: false
---
In the previous post I talked about the simple introduction on how you can
build a computer clock. If you have not read it, [click here](https://wilfred.githuka.com/post/555/).

## Required Components

* R1 - 1kOhm Pull Up Resistor - Control the state of Trigger(PIN2) between 5V and OV.
* R2 - 220Ohm Resistor in series with D1 for overcurrent protection.
* R3 - 1MOhm Resistor for the Discharging/Charging circuit.
* D1 - Yellow LED.
* C1 - 0.1microfarad capacitor(104) - Charging and Discharging capacitor.
* C2 - 0.01microfarad capacitor(103) - Noise reduction capacitor.
* SW1 - Momentary Switch
* NE555 - Main IC

## Concept

This monostable circuit is often called a debouncing circuit since one of its main 
aims is to minimise and reduce a bounce that is created when the switch contacts
come together and bounce instead of making contact at once. This bounce as seen
in an oscilloscope can result in more than one signals to be sent which will be
a headache when debugging the circuit. By using the SR Latch inside the NE555 timer,
I am sure that when I press the button, only a single signal goes through.

## Circuit Theory

![mono-circuit](/img/8/mono_circuit.jpg)

This circuit can only be stable in one state. When the button is pressed, the ciruit comes ON
briefly then goes OFF to the stable state.The duration of the ON state is given by a multiplication
of the Capacitance of C1 and Resistance of R3. For example:

1MOhm(10^6) * 1microfarad(10^-6) = 1 seconds. In this circuit I want it to be as instantaneous as
possible so I change the values to be 1MOhm(10^6) x 0.1microfadad = 0.1 seconds. This means that as
soon as the button is pressed, the output LED comes on.

In the OFF state, the Q output is LOW of OFF, meaning that the Inverted Q is ON. The transistor is also
ON since Inverted Q is ON. There is a current flowing through the transistor which is as a result of the
capacitor C1 and Resistor R3 which as discharging through the transistor. The Threshold(Terminal 6) is
at 0V which is lower than the reference 3.33V along the voltage divider circuit. The comparator is OFF.

At the same time the second comparator is OFF due to the fact that the Trigger(Terminal 2) is ON and at 5V which
is higher than the reference 1.66V required to Turn ON the comparator. There is no input to the SR Latch.

However when the switch SW is closed, the 5V is grounded which makes it fall below the reference 1.667V for the second
comparator, therefore the comparator turns ON and send a signal to the input S of the SR Latch. This sets the
Latch and there is an output at Q resulting to the Inverted Q being turned OFF. The transistor goes OFF and stops conducting.

The capacitor is no longer discharging through the transistor but now charging which causes the Thershold to be at 5V which
is enough to turn ON the comparator which sends a signal to the Reset of the SR Latch. The Latch Resets, turns OFF the Output Q
and goes back to the initial stable state.

The moment the LED goes ON and OFF is as a result of the above process.

![output-curve](/img/8/output_curve.jpg)


