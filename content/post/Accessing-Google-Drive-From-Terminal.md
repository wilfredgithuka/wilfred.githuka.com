---
title: "Accessing Google Drive From Terminal"
date: 2018-05-19T21:25:31Z
subtitle: ""
tags: [archlinux, gdrive]
---
Google Drive is a good way to backup your data. In Windows this can be accomplished simply by having a Google account and drag-dropping stuff into it. From a CLI - Command Line Interface a different approach is used which I will explain in this article.

My distro is [Archlinux]() so this tutorial is based on the same.

## Tools
* rclone
* gdrive

## rclone
rclone is written in Google's Go Language and it a powerful tool that can be used to access your Google Drive neatly from the terminal. rclone features a great interractive config which is easy to use.

### Installation
* sudo pacman -S rclone

### Setup
After installation, run the following command to start the config application.

rclone config
### Usage

rclone ls wilfredrive:

Note: The ls or lsd are different commands. ls will list all files while lsd wil simply list directories. So if you have 12TB of files on your drive, dont run ls as it will take along time to list all the files.

rclone copy image.jpg wilfredrive:

This command will copy image.jpg to the Google Drive

## gdrive
gdrive is a commandline utility for interracting with Google Drive. With gdrive you can upload/download and preety much anything that you would with an external storage location. gdrive can be installed from AUR [here]() 

There is a great tutorial on [Github]() by the creator which goes into detail on how to use it. A typical command looks like:

gdrive upload SampleFile.pdf

grive will then produce an url which when you paste into your browser, Google Drive will ask you to whether you want to grant permission to gdrive, which you will say yes by copying the link back to gdrive in the terminal.

If all match up, then the file upload begins.
