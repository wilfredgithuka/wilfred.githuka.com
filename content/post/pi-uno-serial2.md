---
title: "RaspberryPi Arduino UNO Serial Port Connection"
date: 2018-07-01T13:03:06Z
subtitle: "Connecting the RaspberryPi and Arduino via Serial"
tags: [arduino, pi, c++]
draft: false
---
![sdc](/img/sdc/sdc.jpg)

Our Self Driving Model Car uses a RaspberryPi and Arduino for power and control.
These two powerful and functional devices must have smooth communication else
our car will have control problems thereafter. In our previous car model we used
a RaspberryPi only but now we have an Arduini UNO which will be used to control
the wheels.

Student1: What is the RaspberryPi and Arduino?

The RaspberryPi is a single board, credit card sized computer that runs minimal software and can be used in very many areas. The Arduino is a less powerful development board which is more robust and has I/O pins for Analogue & Digtial I/O

Student2: Can we take out our boards now?

Yes you can.

Your RaspberryPi already has an OS flashed inside(Archlinux ARM), that what I was doing yesterday afternoon. So just power the device from your mobile phone chargers. Open your laptops and ssh into the pi. If you dont know how to do this, please check out this class.

Everybody managed to login?

All Students: Yes

Alright. Now from the terminal run the following command:

```console
sudo lsusb
```
This will list all your USB connected devices. Now also run:
```console
sudo ls /dev/tty*
```
The above commands lists all devices under the tty list. Note the result of the above commands. Now connect the blue short cable to the Arduino.

Run the above commands again and tell me what you see.

Student3: I have a device ttyACM0 showing up

![connecction](/img/sdc/connection.jpg)

Yes thats the Arduino. According to how the Arduino is programmed, it will be on port 24. More details can be found [Here](https://www.teuniz.net/RS-232)

Student2: Why are they called ttyACM0?

The /dev/ttyACM0 is a USB communication device (CDC) of sub-type abtract control model (ACM). This is basically what the Arduino is. The Old D type connector is given the /dev/ttyS0 serial port which is not used much nowadays.

After confirming that the Arduino is showing up on the Raspberry Pi, now download the following [code package](https://www.monocilindro.com/wp-content/uploads/2017/02/Serial_Raspberry_Arduino_20170219s.zip) and extract in in your home folder. You might need to download [unzip](https://www.archlinux.org/packages/extra/x86_64/unzip/) for this task, its a powerful archiver.

Student4: How do I install Unzip?

Simple, just run sudo pacman -S unzip. Provide the password and watch it install. After installation just go to where the .zip code package mentioned above is and run: 

```console
unzip Serial_Raspberry_Arduino_20170219s.zip. 
```

This will create a folder called Serial.

Alright, now go into the Folder /Serial and: 

```console
nano arduino_test.c 
```

We need to make some change here to reflect our port number. Since we are using /dev/ttyACM0 our port number becomes 24. So in this file go to line 11 and change:

```cpp
int cport_nr=16;
```
to be:

```cpp
int cport_nr=24;
```
Thats all now save and close nano. We will now compile the code using gcc which is installed in all your devices.

Now run the following code to compile:

```console
gcc arduino_test.c rs232.c -Wall -Wextra -o2 -o arduino_test
```

Once the program starts, Raspberry Pi keeps sending messages to the Arduino. After sending a message, Pi waits for 1 seconds and then checks if something has been received from Arduino; in positive case, the received message is shown on the display.

Student4: This is amazing :-)

Whats happening is the Raspberry Pi and Arduini are 'talking'. Now for your assignment, try and customise the message, make it personal.

We will end our class here.

All Students: Thank you.
## References
* [Monocilindro Blog](https://www.monocilindro.com/2017/02/19/how-to-connect-arduino-and-raspberry-pi-using-usb-and-c/)
* [Teuniz](https://www.teuniz.net/RS-232/)
* [Arafin's Medium Blog](https://medium.com/@araffin/simple-and-robust-computer-arduino-serial-communication-f91b95596788)
