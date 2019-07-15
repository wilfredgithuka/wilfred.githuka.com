+++
date = "2016-06-16T06:40:51Z"
title = "Connect To Eduroam On Archlinux"
featuredalt = ""
featuredpath = ""
featured = ""
description = "A worldwide internet service for research that is used in universities globally"
categories = ["Linux"]
author = ["Wilfred"]
linktitle = ""

+++

![Example image](/img/2016/eduroam.png)

[Eduroam](https://www.eduroam.org/) is a worldwide internet service for research that is used in universities globally. Eduroam uses a secure protocol when connecting to the users. Windows and other OSs have different configurations. On Archlinux start by running the following commands.

Note: The following steps are for [Connman](https://wiki.archlinux.org/index.php/Connman) (A Daemon for managing internet connections within embedded devices running the Linux operating system. Comes with a command-line client, plus Enlightenment, ncurses, GTK and Dmenu clients are available).

Create a conman directory like below. Case sensitive.

/var/lib/connman

Using your favorite editor, create the following config file

```python
sudo nano /var/lib/connman/wifi_eduroam.config
```
Edit as per your credentials.

```python
[service_eduroam]
Type=wifi
Name=eduroam
EAP=ttls
CACertFile=/etc/ssl/certs/ca-certificates.crt
Phase2=PAP
Identity=username@domain.edu
Passphrase=password
```
I deleted the line CACertFile=/etc/ssl/certs/ca-certificates.crt line so that I could use eduroam in diffrent departments across the university.

Restart the wpa_supplicant.service and connman.service to connect to the new network.

```python
systemctl restart wpa_supplicant
systemctl restart connman.service
```
Your should now be able to connect to eduroam. You can ping my website and update your system to check your connection

```python
sudo ping www.githuka.com
sudo pacman -Syu
```
Using NetworkManager

Click on the Network Manager Applet on the top right hand corner of your screen

Select Eduroam from the list of Wireless Networks

Identity: yourusername@students.ku.ac.ke

Password: yourpassword

Phase 2 Type: MSCHAPv2

Authentication: Protected EAP (PEAP)

Click Connect--Enjoy

