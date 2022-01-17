---
title: Purpose
description: 
published: true
date: 2022-01-17T15:46:19.776Z
tags: 
editor: markdown
dateCreated: 2021-11-12T15:31:30.659Z
---

# Phyllome OS in a nutshell

> *Why would one prefers to use an operating system running in a virtual machine?*

The goal of Phyllome OS is to make it possible to run most operating systems locally on most 
hardware.

## Problematic

An operating system must have drivers to allow it to interact with hardware components and devices such as USB controllers or graphic cards. Each driver has to be specifically written to work with a particular operating system. To support running most operating systems on a specific piece of hardware, one would have to develop and maintain a set of drivers for each one those operating systems, an almost insurmountable task as there are dozen unique operating systems out there.

Most of the time, users pick hardware that ships with their favorite operating system: most hardware is tied to a specific operating system. Therefore, user choice is severely restricted to only a certain set of computers [^1]. Isn’t there a shortcut available, to allow users to run their favorite operating system on most hardware, provided that the operating system license allows it?

[^1]: Popular and proprietary operating systems such as macOS Big Sur or Windows 11 are optimized to only run on a  limited set of computers. This state of affairs significantly limits users’ choice and may incite them to renew their hardware frequently, as operating systems providers may decide to drop support for older hardware models for any number of reasons.

Virtualization provides a partial answer to this problem as it allows the abstraction of the underlying hardware, presenting generic software-based hardware to the operating system. In other words, by means of virtualization, a specific physical computer can be made to look generic to an operating system.

There are many types of virtualization3. Phyllome OS is primarily focused on paravirtualization, which assumes that an operating system running in a virtualized environment is aware of it. For any operating systems to run well in such an environment, one would only have to focus on developing and maintaining a set of generic drivers for virtual hardware, a task that is well under way for many popular operating systems, including Linux-based, Darwin-based or Windows NT-based operating systems

---

*[**Go back to parent page**](https://wiki.phyllo.me/)*