---
author: danfox1982
comments: true
date: 2016-11-03 08:34:30+00:00
layout: post
slug: more-docker
title: More Docker
tags: [Docker]
image:
  feature: banner.jpg
---

[Previously](/2016/09/01/intro-to-docker) I've written about Docker, in particular about how well it works on Windows.  I thought I'd expand on what Docker can give you a little more here, drawn from my own experience.

## Docker? Huh.  What is it good for?

Absolutely anything. Probably.

The easiest way to get fast benefits from Docker while leanring the basics of images and containers etc is to use [Docker Hub](http://hub.docker.com/explore) (soon to be replaced by [Docker Store](http://store.docker.com)).  There are loads of images there ready for use.  Most just need a bit of configuration, typically via environment variables.  Applications such as nginx, haproxy or databases like redis are available for use just by executing `docker run`.  It can make spiking ideas in development no longer require large installs to get going.  Spikes are faster, and ideas can be moved forward or dropped quickly.

There are plenty of supporting tools too, such as [MailCatcher](https://store.docker.com/community/images/yappabe/mailcatcher), which acts as an SMTP server and captures the emails on a website... making testing emails a breeze.  Or maybe a container you could execute daily to make sure your SSL [certificates aren't about to expire](https://store.docker.com/community/images/dariko/docker-ssl-cert-check).

And all of these benefits are available even before you've written a line of code or created a `Dockerfile`.  But what if you want to run a custom container as a supporting tool?  We run a [Hubot](https://hubot.github.com/) to aid our development tasks, and wouldn't want to run it on a development machine so we run it in a [Digital Ocean](https://www.digitalocean.com/) droplet.  Handily, Docker comes with a couple of tools that can help make managing remote containers a little easier.

## Docker Machine

[Docker Machine](https://docs.docker.com/machine/overview/) allows you to point your local CLI to a remote Docker server, meaning that commands - and thus containers - will run on the remote machine.

In order to do this, Docker Machine provides the ability to generate scripts that will set all the necessary environment variables for Docker commands to connect to the remote Docker engine.  Running this line in a bash shell will connect Docker in that shell to a remote server called `dockerhost`.

`eval $(docker-machine env dockerhost --shell bash)`

So now we're able to spin up containers etc on a remote server we could easily just run `docker run` to manually create the containers.  However if you're managing multiple containers, there's an easier way than running many `docker run` commands in the right order.

## Docker Compose

[Docker Compose](https://docs.docker.com/compose/overview/) works by using a configuration file (typically `docker-compose.yml`) to define many containers that work together as a system.  There can even be multiple instances of one image - for example you could have 3 web server containers from a single image, and a load balancer container in front of them.  I often use Docker Compose for single container systems too just for simplicity - it's easier to remember how to run `docker-compose` instead of the exact image name you need for `docker run`.  The `docker-compose.yml` file can also contain [environment variables](https://docs.docker.com/compose/environment-variables/) if you need it to configure the container.

For our Hubot, I always want to run the latest version of our Hubot scripts.  I have no need to keep previous versions etc so the process I follow here is quite brutal - forcing builds and ignoring caches etc.  You'll probably want to change these flags as suits your development lifecycle for your dev tool.

So after running
```shell
eval $(docker-machine env dockerhost --shell bash)
```
to connect Docker to the remote server, run
```shell
docker-compose build --force --no-cache
```
to build the image (if you're not using an image in a repository), then
```shell
docker-compose up --force-recreate --build -d
```
to run the container in detached mode.  You can view logs with
```shell
docker-compose logs -f
```

And that's all there is to it.  I haven't added any examples of `docker-compose.yml` files since the [samples on the Docker website](https://docs.docker.com/compose/compose-file/) are very good.


Enjoy!
