---
title: Get started with Phyllome OS
description: 
published: true
date: 2021-11-23T10:47:06.695Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:37:31.498Z
---

# How to use Phyllome OS daily

*This section explains the "Phyllome OS way of doing things", what you need to do to further configure it, and how to deploy your favorite operating system within it.*   

## Understand the Phyllome OS philosophy

> Phyllome OS has one goal: to let users bring their favorite operating system and to run them well

By definition, the host, Phyllome OS, is trying to be as discrete as possible, so that users won't actually have to spend much time to manage it. Users should be able to spend their time using their favorite personal computing environment, rather than messing around with Phyllome OS itself.[^1] The host is meant to be a great place for guest operating systems to thrive.

Eventually, users will be able to reach *the state of virtual enlightenment* (tm), and stop worrying about the fact that their favorite operating system is running inside a virtual machine, just as humans should stop worrying about living in a computer simulation ([perhaps](https://en.wikipedia.org/wiki/Simulation_hypothesis)).

## Overall view

After Phyllome OS has been successfully installed, a few tasks are required before it can be used to its fullest potential.

* **Run a few post-installation scripts**
* **Create a virtual machine**
  * manually, using `virt-manager` (*default*)
  * automatically, using `virt-install` (*for power users*)
* **Install your favorite guest operating system** inside this virtual machine
  * manually, using the installer provided by the editor of your favorite operating system 
  * automatically, using a kickstart file, for compatible guest systems
* **Learn how make the most out of it**

As Phyllome OS evolves, one of the main goal is to shorten the time it would take for an end-user to have a fully operationnal virtual machine running with favorite operating system optimized virtual machine with their favorite operating system.   

## Post-installation configuration


---

*Are you looking for tasks to do with your system? If so, have a look at doing some of the [suggested tasks](/gofurther)*

[^1]: Although, we very much encourage you to [hack it](https://github.com/PhyllomeOS/phyllomeos#how-to-hack-phyllome-os).