---
title: "Epson L850 Inkjet Printer Driver Installation"
date: 2019-09-05T05:14:30Z
draft: false
---

The Epson L850 is a versatile printer that I came accross recently. Its the kind of
printers that carry along an ink tank which is good but abit messy when it comes to
refilling it.

### Driver Installation

This Driver installation tutorial is for Linux users specifically Archlinux. Am assuming
that the connection media to the printer is via a USB 2.0 cable.

* Update your machine.

```
pacman -Syu
```
* Install [Epson Inkjet Printer Driver](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr/) (ESC/P-R) for Linux.

```
yay epson-inkjet-printer-escpr 
```

* Install Epson L800 Driver packages.

```
yay epson-inkjet-printer-l800
```

After the above installs successfully, you are good to go. Print the test page :-)

The ppd file for most printers is available on this [Github repo](https://github.com/liberodark/Print-PPD).
