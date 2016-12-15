---
author: danfox1982
comments: true
date: 2016-12-15 08:34:30+00:00
layout: post
slug: raspberries-pies-pythons-ansible-and-the-weather
title: Raspberries, Pies, Pythons, Ansible and the Weather
tags: [RaspberryPi, Python, Ansible, Linux]
image:
  feature: banner.jpg
---

I used to own an original [Raspberry Pi Model B](https://www.raspberrypi.org/products/model-b/){:target="_blank"}. I'd bought it as soon as it came out, wondering what I could do with this amazingly small device.  At the time I had very little Linux skills and I was very much a C#-only developer.

It turns out not a lot.  It's absolutely no fault of the fantastic little device, it's just that it can be difficult to work out what you can do with something if you have virtually no idea where to start, what languages to learn or how to go about it in a new operating system.  I ended up following a brilliant tutorial (similar to [this](https://www.raspberrypi.org/learning/python-web-server-with-flask/){:target="_blank"}) on setting up a simple web server using [Flask](http://flask.pocoo.org/){:target="_blank"}... then installed [OpenELEC](http://openelec.tv/){:target="_blank"} and used it as a small media centre for a while before deciding it was a bit underpowered for me and selling it on.

Fast forward a couple of years and a couple of generations of Raspberry Pi and I'm having another go.  I have more knowledge of Linux, non-C# languages and deployment techniques, and the [latest Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/){:target="_blank"} has a bit more horsepower and integrated WiFi.  So with that in mind I set about a new project.  A simple application that can fetch a weather forecast and display a corresponding image on an LED matrix.

I also wanted to use a provisioning tool to configure the system so I can easily wipe the microSD card and start again if I want to.  This would help if I need to replace the microSD card or upgrade the Raspberry Pi in the future.

I chose [Python](https://www.python.org/){:target="_blank"} as the development language as there are a lot of resources on how to write Python on Raspberry Pi, and it is used extensively in DevOps and would be a useful tool to learn.

[Ansible](https://www.ansible.com/){:target="_blank"} is a provisioning tool I'd had a little bit of exposure to and this was a great opportunity to learn more about it.  So far I've found it particularly appealing amongst provisioning tools due to the simplicity of the ssh-based connection and the ability to run simple shell scripts directly.

The weather data is provided by [Dark Sky](https://darksky.net/dev/){:target="_blank"}.  The API is simple to use and 1,000 free queries are permitted per day, which will be fine for a five-minute periodic refresh.

Finally the LED matrix I selected is the [SenseHAT](https://www.raspberrypi.org/products/sense-hat/){:target="_blank"}.  I also looked at the [Unicorn HAT](https://shop.pimoroni.com/products/unicorn-hat){:target="_blank"} which is a similar price but decided the extra features - in particular the joystick for a headless input device - made the SenseHAT a better choice.

All the code is [here](https://github.com/foxy1982/RaspberryPi){:target="_blank"}.  The Python code for the actual program is in the `weather-hat` directory and the Ansible playbooks are in `provisioning`.

The code itself is fairly simple: it queries the Dary Sky API using an API key from an environment variable. The latitude and longitude to use in the query are configured in the same way.  Ansible includes a nice feature called [Ansible Vault](http://docs.ansible.com/ansible/playbooks_vault.html){:target="_blank"} which basically encrypts and password protects variables.  I use this for the API key so replace this with your own if you try it out.  Ansible will prompt for the password for any encrypted files when you run `ansible-playbook`.

The weather images are simple png files which is nice as you can preview them outside of the application.  Initially I had configured them as pixel arrays but this proved difficult to maintain.  If anyone has any idea on how to improve the icons please let me know, artistry isn't my strongest point...!

The provisioning side of it is fairly simple too.  The playbook will install Git and Leafpad onto the Pi to help with editing files should you want to.  It will then install the repo itself (an easy way to get the source code onto the device!) as well as some SenseHAT examples to play around with.  It then installs the weather-hat application as a service and starts it up.  Finally it installs nginx.

There are a few things I'd like to improve in the future:

- **nginx**: I've put the provisioning steps in for nginx but it's not yet being used.  I want to use Flask in the service to allow configuration of the service, such as latitude and longitude.

- **weather modules**: I think there will be a better way to manage the weather modules and images.  At the moment there's an implicit interface to the modules and the need to be loaded in `icon_mapper.py`.  This could probably be changed to a more dynamic loading technique.

- **control**: use the joystick on the front of the SenseHAT to change the displayed data, maybe change the forecast length or move through a set of locations.

So, lots to do, but lots learnt about Python and Ansible already!

Enjoy
