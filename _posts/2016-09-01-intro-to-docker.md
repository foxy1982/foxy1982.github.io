---
author: danfox1982
comments: true
date: 2016-09-01 08:34:30+00:00
layout: post
slug: intro-to-docker
title: Intro to Docker
tags: [Docker]
image:
  feature: banner.jpg
---

[Docker](http://www.docker.com) is a phenomenal technology for a number of reasons, one of which is aiding deployment. It's not for Average Joe to use on his desktop, although with some tweaks and slick UX that could probably change. Whether it needs to go down that route is another question… Desktop apps aren't exactly cutting edge technology these days.

I digress. The fact is that Docker remains a brilliant tool in the developer's toolbox to distribute applications… whether they're production or standalone tools to help development, test or monitoring. I'm not going to dig into what a Docker container or image is here - [other people on the Internet can explain that better and more effectively than I ever could](https://docs.docker.com/engine/userguide/intro/). What I am going to discuss is how it can affect people like me… a Windows developer with bits of Linux knowledge.

One of the downside of working with Docker on Windows is that it doesn't run natively (since Docker leverages some Linux kernel functionality).  It doesn’t work natively on OSX either for that matter. The resulting experience isn't always pleasant as sometimes the VirtualBox VM that Docker runs its containers in can disconnect from the management machine (i.e. the Windows machine) and Docker needs restarting.

There is a newer version called Docker for Windows which is still in beta and it’s definitely much slicker. It feels a lot closer to a native Docker implementation even though it uses the same VM technique, although it uses HyperV instead of VirtualBox. Unfortunately this has pitfalls for me… I have a lot of existing virtual machines that use VirtualBox and as Windows can only run one hypervisor at a time this requires a setting change, a reboot and all the cognitive context switches that go with it. I may as well just create a dual boot machine with Ubuntu as the alternative OS.

None of this should put you off though.  At all.  In general, it works, and it's smooth even if it's not as slick as it is natively in Linux. At some point I'll talk a little bit about managing remote Docker containers, and how simple or complex it can be.
