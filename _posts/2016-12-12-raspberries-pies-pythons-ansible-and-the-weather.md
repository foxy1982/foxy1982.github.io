---
author: danfox1982
comments: true
date: 2016-12-12 08:34:30+00:00
layout: post
slug: raspberries-pies-pythons-ansible-and-the-weather
title: Raspberries, Pies, Pythons, Ansible and the Weather
tags: [RaspberryPi, Python, Ansible, Linux]
image:
  feature: banner.jpg
---

I used to own an original [Raspberry Pi Model B](https://www.raspberrypi.org/products/model-b/){:target="_blank"}. I'd bought it as soon as it came out, wondering what I could do with this amazingly small device.  At the time I had very little Linux skills and I was very much a C#-only developer.

It turns out not a lot.  It's absolutely no fault of the fantastic little device, it's just that it can be difficult to work out what you can do with something if you have virtually no idea where to start, what languages to learn or how to go about it in a new operating system.  I ended up following a brilliant tutorial (similar to [this](https://www.raspberrypi.org/learning/python-web-server-with-flask/){:target="_blank"}) on setting up a simple web server using Flask... then installed [OpenELEC](http://openelec.tv/){:target="_blank"} and used it as a small media centre for a while before deciding it was a bit underpowered for me and selling it on.

Fast forward a couple of years and a couple of generations of Raspberry Pi and I'm having another go.  I have more knowledge of Linux, non-C# languages and deployment techniques, and the [latest Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/){:target="_blank"} has a bit more horsepower and integrated WiFi.  So with that in mind I set about a new project.  A simple application that can fetch a weather forecast and display a corresponding image on an LED matrix.

I also wanted to use a provisioning tool to configure the system so I can easily wipe the microSD card and start again if I want to.  This would help if I need to replace the microSD card or upgrade the Raspberry Pi in the future.

I chose [python](https://www.python.org/){:target="_blank"} as the development language as there are a lot of resources on how to write python on Raspberry Pi, and it is used extensively in DevOps and would be a useful tool to learn.

[Ansible](https://www.ansible.com/){:target="_blank"} is a provisioning tool I'd had a little bit of exposure to and this was a great opportunity to learn more about it.  I found it particularly appealing amongst provisioning tools due to the simplicity of the ssh-based connection and the ability to run simple shell scripts directly.

The weather data is provided by [Dark Sky](https://darksky.net/dev/){:target="_blank"}.  The API is simple to use and 1,000 free queries are permitted per day, which will be fine for a five-minute periodic refresh.

Finally the LED matrix I selected is the [SenseHAT](https://www.raspberrypi.org/products/sense-hat/){:target="_blank"}.  I also looked at the [Unicorn HAT](https://shop.pimoroni.com/products/unicorn-hat){:target="_blank"} which is a similar price but decided the extra features - in particular the joystick for a headless input device - made the SenseHAT a better choice.
