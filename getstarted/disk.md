---
title: Get started with Phyllome OS
description: 
published: true
date: 2021-11-23T13:33:26.183Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:37:31.498Z
---

# How to use Phyllome OS daily

*This section explains how to further configure Phyllome OS, and how to deploy your favorite operating system within it.*   

## Post-installation configuration

After Phyllome OS [has been successfully installed](/deploy/install) and [the first-launch process has been completed](/deploy/install#first-launch), a few tasks are required before it can be used to its fullest potential.

> As Phyllome OS evolves, one of the main goal is to shorten the time it would take for an end-user to have a fully operational virtual machine loaded with the installer of their favorite operating system, to the point that a user may not see the Phyllome OS environnement at all.
{.is-info}

### Grant the current user the ability to manage virtual machines

Any new user, including the one that has been created during the first-launch set up, won't be part of the `libvirt` group. It  means that it won't be able to manage the *qemu:///system*, which runs `libvirt` as root.

To avoid a password prompt each time the Virtual Machine Manager is launched, you can add the current user to the `libvirt` by using the following command, in the terminal:

```
sudo usermod -a -G libvirt $(whoami)
```
> A known bug affects the terminal: extra spaces between letters. To solve it, click on the burger menu (three stacked horizontal lines) then go to *Preferences > Profiles > Unnamed* and check the box called *Custom font*. 
{.is-warning}

### Run a few scripts

During the installation process, a few scripts got fetched. They need to be run to further customize Phyllome OS. 



## What to do next

* **Create a virtual machine**
  * manually, using `virt-manager` (*default*)
  * automatically, using `virt-install` (*for power users*)
* **Install your favorite guest operating system** inside this virtual machine
  * manually, using the installer provided by the editor of your favorite operating system 
  * automatically, using a kickstart file, for compatible guest systems

---

*Are you looking for tasks to do with your system? If so, have a look at doing some [suggested tasks](/gofurther)*

[^1]: Although, we very much encourage you to [hack it](https://github.com/PhyllomeOS/phyllomeos#how-to-hack-phyllome-os).