---
author: danfox1982
comments: true
date: 2016-04-12 08:34:30+00:00
layout: post
slug: return-of-the-amiga
title: Return of the Amiga
tags: [General, Amiga]
image:
  feature: banner.jpg
---

As I've said [previously](/2016/01/12/my-first-girlfriend) I'm the proud owner of an Amiga 1200 and recently challenged myself to get it online with a view to writing some code on it.  I've no idea why I want to do this, other than maybe I feel it's making up for something I should have done as a teenager instead of just playing SWOS and Worms.  And Lemmings.  And Speedball 2.

Well, my Amiga is now online!  It's capable of showing http (no SSL on my Amiga yet) web pages, so I thought this would be a good opportunity to share how I did it.  Here it is (surrounded by junk...):

![Amiga1200]({{ site.url }}/images/amiga.jpg)

The screen was one area where I was really lucky.  The Amiga's standard RGB port is a fairly unique 23-pin D-SUB, and outputs at a non-standard refresh rate by default (15KHz).  Luckily for me, I already had a Benq monitor which supports this refresh rate, and a standard 15-pin VGA D-SUB input, and a 23-pin to 15-pin VGA cable.  Result!

One crucial thing a stock Amiga 1200 needs before getting online is a network connection.  I added an ethernet port using the PCMCIA slot on the side of the machine.  I decided to get a wired network card instead of a wireless one, purely because I knew that the configuration would be hard enough without having to fight different standards of wireless network.  Anything I could do to make my challenge easier was a bonus :-)

In terms of hard drive, I had already upgraded the machine to use a 4GB Compact Flash card.  Setting it up wasn't trivial but there are some excellent guides on the internet (such as [this one](https://16bitdust.wordpress.com/2015/10/13/partitioning-16-gb-compact-flash-card-with-winuae-and-pfs3/)) that will help guide how to do it using WinUAE, which is faster and saves wear and tear on your floppy drive :-D

A basic 1200 would struggle to run an OS, TCP/IP stack and web browser - remember we're talking about a machine that has 2MB of RAM and a CPU that runs at 14MHz... that's not a lot of juice, especially the RAM (a slow processor just means things take longer!)  A couple of years ago I bought an 8MB RAM card that sits in the trapdoor slot so I could play some games.  Initially I thought this would be enough, however due to the was memory addressing works with the Amiga 1200 and the PCMCIA slot I was limited to using only 4MB of RAM from the expansion card - 6MB in total.  I decided to upgrade to an ACA1221 and now my Amiga runs at 28MHz with 63MB RAM, more than enough to run the network stack and browser!  Here's what the ACA1221 looks like:

![ACA1221]({{ site.url }}/images/aca1221.jpg)

Getting the PCMCIA card and ACA1221 expansion working smoothly at startup involved some changes to the startup-sequence file.  That's the file that the Amiga executes to configure the system.  For anyone that's interested, these are the top few lines of the startup-sequence... I'll explain the settings in a future post:

```
; Added by NETPCM00X-Installer
C:CardPatch
run >NIL: C:CardReset TICKS 50

; ACA1221
IF EXISTS C:ACATune
  ACATune -vbrmove -maprom * -cache on -burst on >RAM:boot-acatune.txt
ENDIF

IF EXISTS C:ACAControl
  ACAControl s 3 >RAM:boot-acacontrol.txt
ENDIF
```

In terms of software, I started off using the excellent [ClassicWB](http://classicwb.abime.net/) downloads... a brilliant starting point as the images include a lot of tools you take for granted in modern operating systems - such as Directory Opus.  I use EasyNet for the TCP/IP stack and a demo of iBrowse for browsing as I've found it to be the most stable browser - though I suspect a lot of that might be due to the fact my setup is missing an FPU.

Here's an image of the well-known Google search page:

![Google]({{ site.url }}/images/amiga_google.jpg)

Such a delightful shade of yellow.