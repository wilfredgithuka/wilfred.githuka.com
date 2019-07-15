---
title: "Rooting Sony Xperia M2 Dual 2302"
date: 2017-08-08T11:18:40+03:00
subtitle: ""
draft: true
tags: []
---

## Fastboot

Fastboot (as well as ADB) is included in the [android-tools](https://www.archlinux.org/packages/?name=android-tools) package.


The Big Picture

Android consists of three parts relevant to rooting

the bootloader
recovery system
main system
typically only the main system is running, that is the Linux Kernel, the launcher, the phone app etc.. If we talk about rooting, that means we want to add an additional app to the main system which has access to secured parts of the system and acts as a gatekeeper for other apps that also want to get access.

The problem is the secured parts of the system are locked down – otherwise they would not be secure. This means that we can not simply install that app (e.g. an apk) from within the main system.

Therefore we have to go one level down. This is where the recovery system is. Typically you do not see it, as it is only active when the main system can not run – either because a system update is installed or because you do a factory reset.
As the recovery system can do a full system update, it means that it has also access to the secured parts of the main system – exactly what we need.
The stock recovery system obviously does not allow altering the main system – otherwise everybody could get your private date if you lose your phone.
So we need to replace it as well. But before that we have to talk about the bootloader.

The bootloader is a tiny piece of software which decides whether to start the recovery or the main system (or another main system, like Ubuntu Phone).
In the default configuration in only starts systems that it knows and trusts. In this configuration the bootloader is called locked.
Although this prevents malicious software to change the phone and spy on us, it also prevents us from replacing the recovery system. By the way, this concept is also coming to the PC where it is called UEFI secure-boot.

So what we need to do in order to get root access is

unlock the bootloader
replace the recovery system
install a superuser app

Note that unlocking the bootloader also allows attackers to circumvent any of the android security features (PIN etc). It becomes possible to access all the files on the device using a different recovery system. (unless userdata is encrypted)
Therefore android will wipe all userdata when the bootloader state is changed from locked to unlocked.

Sony Xperia devices don’t ship with a pre-installed recovery. So unless you’ve installed a custom recovery like CWM or TWRP on your device, you won’t be able to boot into recovery mode.

So if you lose your unlocked device or it gets stolen, you better hope the thief is not tech savvy.

## Preparations

First you need to install the fastboot binary to be able to perform low-level communication with the device

apt-get install android-tools-fastboot

Next you have to allow non-root users to execute commands over USB, so you do not have to run fastboot as root.

## Device Check
In your device, open the dialler and enter *#*#7378423#*#* to access the service menu.
The  go to configuration and there down it should read 

Rooting Status:
Bootloader unlocked: Yes

If it says No, or if the status is missing, your device cannot be unlocked.

### Receive Unlocking Key From Sony

On your device, turn on USB debugging by going to Settings > Developer options and click to enable USB debugging.

If your device is Android Jelly Bean 4.2 or newer: Developer options are hidden by default. To enable, tap on Settings > About Phone > Build Version multiple times. Then, turn on USB debugging by going to Settings > Developer options.

## On Phone

* Turn off your Xperia™ M2 dual.
* Connect a USB-cable to your computer.
* On your Xperia™ M2 dual, press the Volume up button at the same time as you connect the other end of the USB-cable.
* Phone will show a blue notification light

sudo fastboot oem unlock 0x[KEY] where <KEY> is the key you obtained.


# References

* https://developer.sonymobile.com/unlockbootloader/
* http://www.rojtberg.net/668/how-to-root-android-using-ubuntu/comment-page-1/
