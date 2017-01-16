---
layout: post
title: OSX File System Basics
date: 2014-01-19 03:31:04
categories: MacOSX
---

> Years ago, when he mentioned about Unix/Linux to his friends, you could saw the admiration in their eyes. However, the word(Unix/Linux) itself is almost all he knew about Unix/Linux.

Time to make a change.

### Why focusing on OSX ?

Here I focus on Max OSX instead of Unix/Linux basically for two reasons :

1. OSX has the second largest desktop OS market share ([7.53%](http://http://en.wikipedia.org/wiki/Usage_share_of_operating_systems "os market share")). First is of course Windows, some old stuff.
2. OSX is Unix based. If we know about OSX, we somewhat know about Unix.

### Preparations to see OSX file system

Seeing is believing. Before talking about how the file system looks like, let's find it first. (Starters always find hard time looking for the file system.) Here are the steps:

1. Search and open `Terminal` in Spotlight (on the right corner of your screen).
2. Type in `cd /` in terminal. This could led you to the **root of the file system**, and welcome to the **bottom of the world**!
3. Type in `ls`. This command would show you how the **world** looks like.

After these three steps, you would get everything as follows

```bash
Applications User Information dev opt var
Incompatible Software Users etc private
Library sbin Network bin tmp System usr
```

### Decompose OSX File System

Type in `ls <folder name>` to see what's inside the folder. For example, `ls home`. Here, I only choose the most important ones from in the root folder.

| Directory | Description |
| --------- | ----------- |
| /Applications | includes all the applications you installed. |
| /Users | includes users of the computer. |
| /tmp | temporary directory to store temporary files. files are deleted from /tmp upon reboot. |
| /Volumes | mount CDs/DVDs/Hard Drive and etc. your hard drive, flash drive, DVDs would are here. |
| /dev | device files. it's where mouse, keyboard and other peripheral devices are kept. |
| /mach_kernel | the kernel of OS. the foundation or the heart of Mac OSX. |
| /Library | includes system settings, preferences and other essential files for OS. |
| /usr | includes subdirectories that contain information, configuration files, and other essentials used by the operating system. |
| /usr/bin | different from /bin, it includes less commonly used unix commands. |
| /bin | bin is short for **binary**, it includes most commonly used unix commands. |
| /etc | contains configuration files of the system |
| /sbin | it is like /bin except it contains binaries that are specifically used for system administration |
| /var | `/var` is short for **variable**. it stores variable files. processes like printing and programs that store log files will use subdirectories in the /var directory to store those files. |
