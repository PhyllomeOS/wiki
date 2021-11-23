---
title: Get started with Phyllome OS
description: 
published: true
date: 2021-11-23T11:25:51.814Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:37:31.498Z
---

# How to use Phyllome OS daily

*This section explains the "Phyllome OS way of doing things", what you need to do to further configure it, and how to deploy your favorite operating system within it.*   

## Understand the Phyllome OS philosophy

> *Phyllome OS has one goal: to let users bring their favorite operating system and to run them well. Eventually, users should be able to reach **the state of virtual enlightenment** (tm), and stop worrying about the fact that their favorite operating system is running inside a virtual machine, just as humans should stop worrying about living in a computer simulation* ([perhaps?](https://en.wikipedia.org/wiki/Simulation_hypothesis)).

By definition, the host, Phyllome OS, is trying to be as discrete as possible, so that users won't actually have to spend much time to manage it. Users should be able to spend their time using their favorite personal computing environment, rather than messing around with Phyllome OS itself.[^1] 

However, if the host is meant to be a great place for guest operating systems to thrive, it is up to the user to manage the lifecycle of their guest operating system. Phyllome OS provides an optimized virtual machine model tuned to host modern operating systems, but at the exeption of some RPM-based guests operating systems including Phyllome OS itself, does not intent to provide automated ways to deploy guest operating systems (such as [Infrastructure as code solutions](https://en.wikipedia.org/wiki/Infrastructure_as_code) or an instance initialization software like [cloud-init](https://github.com/canonical/cloud-init)). 

In other words, contrary to end-to-end operating systems like [Qubes OS](https://www.qubes-os.org/) or the upcoming [Spectrum](https://spectrum-os.org/), which are offering ready to use templates or/and applications isolated in virtual machines by default, Phyllome OS delegates to end-users the task to install their favorite operating system, while trying to provide the best possible defaults for each operating system. In this regard, its model is closer to [Promox](https://www.proxmox.com/en/), which doesn't make assumptions about how an operating system will be deployed.

## Post-installation configuration

After Phyllome OS [has been successfully installed](/deploy/install) and [the first-launch is process is done](/deploy/install#first-launch), a few tasks are required before it can be used to its fullest potential.

> As Phyllome OS evolves, one of the main goal is to shorten the time it would take for an end-user to have a fully operational virtual machine loaded with the installer of their favorite operating system, to the point that a user may not see the Phyllome OS Desktop environnement at all.
{.is-info}

### Post-installation scripts


## What to do next

* **Create a virtual machine**
  * manually, using `virt-manager` (*default*)
  * automatically, using `virt-install` (*for power users*)
* **Install your favorite guest operating system** inside this virtual machine
  * manually, using the installer provided by the editor of your favorite operating system 
  * automatically, using a kickstart file, for compatible guest systems
* **Learn how to make the most out of it**

---

*Are you looking for tasks to do with your system? If so, have a look at doing some of the [suggested tasks](/gofurther)*

[^1]: Although, we very much encourage you to [hack it](https://github.com/PhyllomeOS/phyllomeos#how-to-hack-phyllome-os).