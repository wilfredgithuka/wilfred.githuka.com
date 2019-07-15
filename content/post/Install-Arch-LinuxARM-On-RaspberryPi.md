+++
date = "2015-12-21T05:45:15Z"
title = "Install Arch LinuxARM On RaspberryPi"
linktitle = ""
description = "Install Arch LinuxARM On RaspberryPi Credit Sized Computer"
categories = ["Linux"]
author = ["Wilfred"]
featuredalt = ""
featuredpath = ""
featured = ""

+++
![Example image](/img/2015/Raspberry-Pi.jpg)

The Raspberry Pi is an ARM v6 architecture mini computer that gained alot of fame when it was released in 2012.

# Formating the SD Card

Start fdisk to partition the SD Card. Then type the following:
```python
o - Delete any partitions on the SD Card.
p - List all partitions, at this point there should be none left.
n then p for primary, 1 for the first partition, press ENTER to accept the default first sector, then type +100M for the last sector.
t, then c to set the first partition to type W95 FAT32(LBA)
n, then p for primary, 2 for the second partition on the drive, and then press ENTER twice to accept the default first and last sector.
w, to write to the partition table.
```
# Mounting & Creating the File System

When you run lsblk it should print out the disk map on your pc. The memory card should be sdb1 and sdb2 for the 2 partitions.

```python
mkfs.vfat /dev/sdb1
mkdir boot
mount /dev/sdb1 boot
```
```python
mkfs.ext4 /dev/sdb2
mkdir root
mount /dev/sdb2 root
```
# Downloading & Extracting The File System

Warning: This has to be done as root and not sudo. So log-off the current user and log-in as root.
```python
#su root
```
Now as root, lets continue to download the packages. If you don't have wget installed, install it first.
```python
wget http://archlinuxarm.org/os/ArchLinuxARM-rpi-latest.tar.gz
bsdtar -xpf ArchLinuxARM-rpi-latest.tar.gz -C root
sync
```
# Moving Files to boot Partition

The following bash statement will move the files, may take some few minutes.
```python
mv root/boot/* /boot
```
Un-mount the 2 partitions.
```python
umount boot root
```
# Housekeeping

Use terminal or SSH to login via the IP Address given by your router.

User-name is: alarm 

Password: alarm

Root account is: root 

Password: root
