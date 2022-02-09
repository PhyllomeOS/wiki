---
title: Purpose
description: 
published: true
date: 2022-02-09T20:19:32.002Z
tags: 
editor: markdown
dateCreated: 2021-11-12T15:31:30.659Z
---

# Phyllome OS in a nutshell

The goal of Phyllome OS is to make it possible to run most operating systems locally on most hardware.

## Problematic

Most PC hardware is designed to work with a single operating system. Since the beginning, the end-users' freedom is serverly restricted, as the operating system is almost always preinstalled.[^1] Isn’t there a way to allow users to run their favorite operating system on most hardware?

[^1]: Popular and proprietary operating systems such as macOS Big Sur or Windows 11 are optimized to only run on a limited set of computers. This state of affairs significantly limits users’ choice and may incite them to renew their hardware frequently, as operating systems providers may decide to drop support for older hardware models for any number of reasons.

[Virtualization](/virt/lexicon#virtualization) provides a partial answer to this question as it allows the abstraction of the underlying hardware, presenting generic software-based hardware to the operating system. In other words, by means of virtualization, a specific physical computer can be partially abstraced away and made to look generic to an operating system.

To be compatible with physical hardware, including USB controllers or graphic cards, one would still need to use a base operating system that can provide software to drive these physical devices.[^3] Most Linux distributions, including Fedora or Debian, ship with a large selection of such drivers, and as such represent another part of the solution to this problem.[^4] 

[^4]: The industry is even developing drivers for Linux first, at least for certain categories of components such as Network Interface Cards (NICs).

[^3]: An operating system must possess drivers to allow it to interact with hardware components, devices or peripherals such as storage controllers, graphic cards or keyboards. Each driver has to be specifically written to work with a particular operating system. A specific piece of hardware requires a specific driver tailored for each operating systems out there. Achieving support across operating systems is an almost insurmountable task as there are dozen unique operating systems out there.

## In summary 

The idea behind Phyllome OS is to rely on Linux to provide drivers for specific hardware components and virtualization[^5] to provide a limited set of generic virtualized hardware that are already or could be made to work with most operating systems. The burden of hardware compatibility is put on Linux, freeing the operating system underneath, which would only need to provide generic virtual hardware drivers[^2].

[^5]: There are many types of virtualization. Phyllome OS is primarily focused on paravirtualization, which assumes that an operating system running in a virtualized environment is aware of being virtualized. For any operating systems to run well in such an environment, one would only have to focus on developing and maintaining a set of generic drivers for virtual hardware, a task that is well under way for many popular operating systems, including Linux-based, Darwin-based or Windows NT-based operating systems.

[^2]: For instance, to provide storage block capacity, a developer of a specific operating system like Sculpt OS or ReactOS would only need to develop support for virtio-blk for its environment, and resort to Linux to interact with the hardware directly.

Technically speaking, Phyllome OS is an operating system, a free and open source Linux distribution, a Fedora Remix based on Fedora Server designed to leverage hardware-assisted virtualization to run graphically-accelerated UNIX and non-UNIX-based operating systems locally, in a virtual machine, using off-the-shelf hardware and open source software.


---

*[**Go to parent page**](https://wiki.phyllo.me/phyllomeos)*