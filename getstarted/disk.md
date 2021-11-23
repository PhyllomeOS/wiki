---
title: Get started with Phyllome OS
description: 
published: true
date: 2021-11-23T15:12:13.472Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:37:31.498Z
---

# How to use Phyllome OS

*This section explains how to further configure Phyllome OS, and how to deploy your favorite operating system within it.*   

## Post-installation configuration

After Phyllome OS [has been successfully installed](/deploy/install) and [the first-launch process has been completed](/deploy/install#first-launch), a few tasks are required before it can be used to its fullest potential.

> As Phyllome OS evolves, one of the main goal is to shorten the time it would take for an end-user to have a fully operational virtual machine loaded with the installer of their favorite operating system, to the point that a user may not see the Phyllome OS environnement at all.
{.is-info}

> The following post-instalaltion configuration will, hopefully, be made obsolete in a future Phyllome OS version. 
{.is-info}

### Grant the current user the ability to manage virtual machines

Any new user, including the one that has been created during the first-launch set up, won't be part of the `libvirt` group. It  means that it won't be able to manage the *qemu:///system*, which runs `libvirt` as root.

To avoid a password prompt each time the Virtual Machine Manager is launched, you can add the current user to the `libvirt` by using the following command, in the terminal:

```
sudo usermod -a -G libvirt $(whoami)
```
> A known bug affects the terminal: extra spaces between letters. To solve it, click on the burger menu (the three stacked horizontal lines) then go to *Preferences > Profiles > Unnamed* and check the box called *Custom font*. 
{.is-warning}

> Phyllome OS will eventually switch to the *qemu:///session* URI, which doesn't require elevated privileges. Have a look at [this great blog post](https://blog.wikichoon.com/2016/01/qemusystem-vs-qemusession.html) to understand some of the differences between the *session* and the *system* URI.  
{.is-info}

### Run a few scripts

During the installation process, [a few scripts are fetched](https://github.com/PhyllomeOS/phyllomeos/tree/main/post) and stored under the `/usr/sbin` directory. They need to be run to further customize Phyllome OS.

#### Desktop enhancements

The following script will change the desktop background and pick opinionated defaults for the Virtual Machine Manager. It will also add a new User session URI for the Virtual Machine Manager. 

Open the terminal and run the following script as a regular user:

```
/usr/sbin/configure-vmm-and-desktop.sh
```
#### Create a virtual machine

The following script, which also doesn't require root privileges, will create a virtual machine called `my-first-live-vm`. This virtual machine will start automatically and will be added to `virt-manager`.

```
/usr/sbin/create-live-vm.sh
```

> That's it, congratulations! 
{.is-success}

## Access your virtual machine display




---

*Are you looking for tasks to do with your system? If so, have a look at doing some [suggested tasks](/gofurther)*

[^1]: Although, we very much encourage you to [hack it](https://github.com/PhyllomeOS/phyllomeos#how-to-hack-phyllome-os).