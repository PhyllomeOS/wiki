---
title: Get started with Phyllome OS
description: 
published: true
date: 2022-01-12T20:39:06.191Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:37:31.498Z
---

# How to use Phyllome OS

*This section explains how to further configure Phyllome OS and how to use in a general sense.*   

## Post-installation configuration

After Phyllome OS [has been successfully installed](/deploy/install) and [its first-launch process completed](/deploy/install#first-launch), a few tasks are required before it can be used to its fullest potential.

> As Phyllome OS evolves, the following post-installation configuration will, hopefully, be made obsolete 
{.is-info}

### Grant the current user the ability to manage system-based virtual machines

Any new user, including the one that has been created during the first-launch set up, won't be part of the `libvirt` group. It  means that it won't be able to manage the *qemu:///system*, which runs `libvirt` as root.

To avoid a password prompt each time you connect to *qemu:///system*, you can add the current user to the `libvirt` by using the following command, in the terminal:

```
sudo usermod -a -G libvirt $(whoami)
```

> Phyllome OS will eventually switch to the *qemu:///session* URI, which doesn't require elevated privileges. Have a look at [this great blog post](https://blog.wikichoon.com/2016/01/qemusystem-vs-qemusession.html) to understand some of the differences between the *session* and the *system* URI.  
{.is-info}

### Update GRUB and reboot

Unfortunately, the GRUB config won't correctly update during the kickstart phase, so it has to be done manually.

```
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```
When the is done, please reboot: `sudo reboot`

## Install and use a guest operating system

Generally speaking, installing your favorite guest operating system inside Phyllome OS requires that you fetch an official ISO from the editor of the said operating system, that you make it accessible to `libvirt` and that you go through the installation.

>  Under construction
{.is-warning}

---

*Are you looking for tasks to do with your system? If so, have a look at doing some [suggested tasks](/gofurther)*

[^1]: Although, we very much encourage you to [hack it](https://github.com/PhyllomeOS/phyllomeos#how-to-hack-phyllome-os).