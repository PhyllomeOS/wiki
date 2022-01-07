---
title: Understand what you are signing up for
description: 
published: true
date: 2022-01-07T10:52:31.901Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:19:38.215Z
---

# Is Phyllome OS right for you?

## Phyllome OS Philosophy

> Phyllome OS has one primarly goal: *to let users bring their favorite operating system and to run them well*.

* The host, Phyllome OS, is designed to be as discrete as possible.
* Phyllome OS should mostly take care of itself, so that users can spend their time using their favorite personal computing environment. 
	* That being said, we very much encourage users to [hack it](https://github.com/PhyllomeOS/phyllomeos#how-to-hack-phyllome-os), suggest new features and report bugs using [the issues system](https://github.com/PhyllomeOS/phyllomeos/issues).
* Eventually, users should be able to reach *the state of virtual enlightenment* (tm), which means accepting the fact that their favorite operating system is running inside a virtual machine, and being able to take advantage of that state of affairs.

> Phyllome OS has just started its journey and there is still a long, *years-long*, way to go to achieve its vision. It has several, [critical]() limitations.  
[Support](/virt#guests) for guest systems differs widely. Have a look there 
{.is-warning}

## Phyllome OS versions

### Versions

Phyllome OS exists in two main versions: **Phyllome OS Desktop**, which features a graphical desktop environment, and **Phyllome OS Server**, which does not. Phyllome OS Server is made for power users. It includes all virtualization enhancements that Phyllome OS Desktop provides, without the GNOME-based desktop environment. 

If you don't know which one to choose, you should probably pick the Desktop version, which in turns comes in many flavors. There is a generic one, Phyllome OS Desktop, without out-of-the box support for nested virtualization. There are also other editions optimized for a particular combination of hardware.

|  | GPU-agnostic | Intel's graphics cards | AMD's graphics cards | Nvidia's graphics cards | 
|---|---|---|---|---|
| *Intel CPU* | N/A | Phyllome OS Desktop II | Phyllome OS Desktop IA | Phyllome OS Desktop IN |
| *AMD CPU* | N/A | Phyllome OS Desktop AI  | Phyllome OS Desktop AA | Phyllome OS Desktop AN |
| CPU-agnostic | Phyllome OS Desktop | N/A  | N/A | N/A |

> The first letter refers to the CPU manufacturer, the second letter to the GPU manufacturers.
{.is-info}

Depending on your hardware, you need to pick the right edition. For example, if you possess an Intel CPU and an AMD graphics card, you should pick either Phyllome OS Desktop IA or Phyllome OS Server IA.

> As of now, **only Phyllome OS Desktop II is supported**. In other words, as of now, you need to use a computer with both an Intel CPU and an Intel GPU to leverage Phyllome OS. Support for other other editions are expected for the Beta.  
{.is-info}

> **Still undecided?** You can give Phyllome OS a try, as a live system booting off from a USB thumb drive, without impacting the existing operating system on your machine.

---

*Please go to [the next section](/deploy/prepare) to prepare your host computer.*

