+++
linktitle = ""
categories = ["Linux"]
title = "The I Love Candy Pacman Mod"
featuredpath = ""
description = ""
author = ["Wilfred"]
date = "2016-06-14T05:25:16Z"
featuredalt = ""
featured = ""

+++
[Pacman](https://wiki.archlinux.org/index.php/pacman) is the official package manager for [Archlinux](https://www.archlinux.org/). Sometimes its boring watching the Hashes which are used to show progress when Pacman is downloading/working. This kind of user interface has a new mod that shows a capital C eating small things during the progress.

Modify the Pacman config file using your favorite editor.

sudo nano /etc/pacman.conf

Go down to Misc Options and add the word ILoveCandy to the end of the list.

```python
# Misc options
#UseSyslog
#Color
#TotalDownload
CheckSpace
#VerbosePkgLists
ILoveCandy
```
Save the changes and it will take effect immediately.
