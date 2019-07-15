+++
date = "2016-07-18T04:59:55Z"
title = "Youtube-dl"
author = ["Wilfred"]
featuredpath = ""
featured = ""
linktitle = ""
description = "A command-line program to download videos from YouTube.com and a few more sites"
categories = ["Linux"]
featuredalt = ""

+++

![Example image](/img/2016/Youtube-install.png)

# Introduction

Youtube-dl is a command-line program to download videos from [Youtube](http://www.youtube.com) and a few more sites. It requires the Python interpreter (2.6, 2.7, or 3.2+), and it is not platform specific. youtube-dl should work in your Unix box, in Windows or in Mac OS X. It is released to the public domain, which means you can modify it, redistribute it or use it however you like.

# Installation
To install it right away for all UNIX users (Linux, OS X, etc.), type:

```python
sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl
sudo chmod a+rx /usr/local/bin/youtube-dl
```
If you do not have curl, you can alternatively use a recent wget:

```python
sudo wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl
sudo chmod a+rx /usr/local/bin/youtube-dl
```
Archlinux users can install it directly from pacman. 1.47MB

```python
sudo pacman -S youtube-dl
```

# Usage
youtube-dl [OPTIONS] URL [URL...]

There is a massive list of configs which you can apply to youtube-dl. They are available in the Github page.
