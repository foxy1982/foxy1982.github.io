---
author: danfox1982
comments: true
date: 2016-05-18 08:34:30+00:00
layout: post
slug: backing-up-the-amiga
title: Backing up the Amiga
tags: [General, Amiga]
image:
  feature: banner.jpg
---

One of the things that worried me a bit while I was [getting my Amiga online](/2016/04/12/return-of-the-amiga) was what would happen if something went wrong?  Workbench is an operating system that I don't know very much about, so I was very concerned that by installing something incorrectly, copying a file to the wrong folder or incorrectly editing a config file (I don't find the standard text editor, [`ed`](http://wiki.amigaos.net/wiki/AmigaOS_Manual:_AmigaDOS_Using_the_Editors), to be particularly user-friendly) I could break my installation.

What I really needed was a way of backing up the CF card that had the installation on.  I wasn't sure of an easy way to do this using Windows, but luckily [my Mac](/2015/03/23/my-mac-mini) (with it's Unix-esque OS) came to the rescue!

Firstly, you'll need to find the device that represents the CF card.  To do this use the `diskutil` command:

```
diskutil list
```

In my case, the device is `/dev/disk7`.  Yours is likely to be different, and may changed when disconnected, so make sure you choose the correct device.  To create a backup image of the device, use `dd`:

```
dd if=/dev/disk7 of=./workbench3_1.img
```

`if` is the input (in this case my CF card), and `of` (the output location) is a local disk file

You'll also need to know how to restore an image. It goes without saying that this will wipe all data on the device, so proceed at your own risk... and make sure you have the right device!

First, you'll need to unmount the device, and then use `dd` to copy the image on to the CF card

```
diskutil unmountDisk /dev/disk7
dd of=/dev/disk7 if=./workbench3_1.img
```

Good luck!
