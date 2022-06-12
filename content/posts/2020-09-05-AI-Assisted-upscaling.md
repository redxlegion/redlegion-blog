---
title: "AI Assisted Upscaling"
date: 2020-09-05T11:55:13-04:00
comments: true
tags:
- AI
- Lasagne
- docker
- neural-enhance
- python
categories:
- info
---

So this is "in the works", I haven't succeeded yet. The ultimate goal is to be able to upscale a shitty 70kb jpeg to a megapixel jpeg using trained neural networks. Badass, rite? Well, the disclaimer here is that I've been chipping away at this project and haven't yet got a functioning setup. So without further ado, here's my fucking trainwreck.

I started off following the guide at [alexjc/neural-enhance](https://github.com/alexjc/neural-enhance). My first attempt involved me thinking I was slick and I could just grab the docker container since it's already installed, configured, and the neural networks trained with more than a few already very usable targets. 

So we do a `docker run --rm -v `pwd`:/ne/input -it alexjc/neural-enhance --help` and we get the very useful help information from the AI upscaler. Good start, right?

So docker is cool, but it's also a useless piece of shit, because it's self contained and has zero useful facilities in sucking in files from filesystems that aren't virtual. Docker is basically trash for 90% of what you want to do with a computer. Good job, guys. Abstract away all the use a computer has.

So I bang in `docker run --rm -v test.jpg:/ne/input -it alexjc/neural-enhance ${pwd}\test.jpg --zoom=4` because I'm lazy and stupid, and I'm met with this:

![fuck docker](/img/2020/fuckdocker.png)

Awesome, right? I'm sure it's just some dumb shit I'm missing because docker isn't actually platform independent, it just pretends it is. Whatever. Let's do this shit the hard way.

_**So I start perusing the installation of the main library, Lasagne**_

Fuck. Go back. Go back go back go back.

I think I got about as far as training the multi layer process network and it took fucking forever, and that's where I left off last night. No idea if it was successful, as my computer rebooted through the night for some reason. Probably a segfault from training the neural network. Fuck. I haven't started to pick it back up yet, and honestly I'm not super motivated to. For the moment I'm going to do some AI upscaling, but I'm going to lean on one of the webservices, because fuck that. However, I do fully intend to succeed in getting this working. It's going to take some time, but I'll report back with my notes and an example image or two.
