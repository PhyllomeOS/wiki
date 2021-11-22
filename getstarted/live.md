---
title: Get started with the Live system
description: 
published: true
date: 2021-11-22T14:35:43.128Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:36:55.647Z
---

> Section under construction
{.is-warning}

# Phyllome OS as a live system

> Phyllome OS is not production-ready, let alone ready to be used daily as a live system.
{.is-warning}

Using Phyllome OS as a live system is a great way to test it out and make sure your host computer is up to the task, before committing to a [permanent installation](/deploy/live), which is currently the recommended way to use Phyllome OS.

Under certain conditions, you may want to use a live system daily, provided that the disk and [XML configuration](/virt/xml) of your virtual machine disks are stored outside the USB thumb drive.

## Boot from a USB flash drive

By default, when a computer boots up, it will look for an operating system on the internal storage device first. If there is one, it will load this operating system and ignore any other media, such as any USB flash drive that may be plugged to the computer.

To boot from a USB flash drive, one would have to either temporary or permanently alter the so-called boot order. The boot order instructs at what point and where it should look for an operating system. The following section illustrates how to change the boot order *temporary*.

> The process to change the boot order depends on your current computer platform. Please follow the instruction that matches your platform.
{.is-info}

> Booting from a USB flash drive is a **non-destructive** process, which means that it won't affect any pre-existing operating system that may be installed on your computer. As a precautious, it may be good to backup your data or, even better, to use a computer with no personnal data on it.
{.is-info}

### macOS

* Make sure that your computer is turned-off. 
* Locate the <kbd>Alt</kbd> / <kbd>Option</kbd> key on your keyboard.
* Turn your computer on and immediately press the <kbd>Alt</kbd> / <kbd>Option</kbd> key continuously.
* The startup manager should appear after a few seconds.
* Click on the option called *EFI* to boot Phyllome OS. 

> Other Mac startup key combinations can be found [here](https://support.apple.com/en-us/HT201255). 
{.is-info}

### Windows 8 and later versions

> Section under construction
{.is-warning}

### Other computers

> Section under construction
{.is-warning}

## Use it daily

>  At the moment, changes applied to a Phyllome OS Live medium do not persist across reboots.
{.is-info}


---

*Are you looking for things to do with your live system? If so, have a look at doing some [suggested tasks](/gofurther)*