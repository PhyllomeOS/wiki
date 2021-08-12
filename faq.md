---
title: Frequently asked questions
description: This page intents to give answers to common questions around Phyllome OS
published: true
date: 2021-08-12T14:33:17.495Z
tags: info
editor: markdown
dateCreated: 2021-06-19T13:20:00.698Z
---

### Can you explain the whole project and its expected outcome(s) ?

Traditionally, operating systems (OS) installed directly on physical hardware have unfiltered access to the underling system hardware, which they trust by default. In contrast, when deployed inside virtual machines, this access can be mediated at the hypervisor/host level, enhancing the security of the overall system by allowing the user to distrust parts of the hardware stack, a vision that is implemented thorougly by the [QubesOS](https://www.qubes-os.org/), which Phyllome OS draws inspiration from.

Despite these advantages, most individuals don't use a virtual machine as their main desktop OS. One of the reasons is that granting a virtual machine 3D capabilities — a must-have to achieve optimal performance on any desktop environment — is still difficult, prone to errors, and risky from a security standpoint as it increases the attack surface of the overall system.

The goal of Phyllome — which is in its very early stages — is to develop and distribute a KVM/QEMU-powered Linux distribution built on a small set of software and that will allow the virtualization of 3D accelerated guest operating systems out-of-the-box, including non-UNIX ones, while offering better security and privacy than OS installed directly on physical hardware.

### How the fuck will make any money with that project ?

I don't give a shit, do you? 

### What does Phyllome mean ?

According to the [Wiktionnary](https://en.wiktionary.org/wiki/phyllome), phyllome means  
> a foliar part of a plant; any organ homologous with a leaf, or produced by metamorphosis of a leaf.

### When will it be released ?

The alpha is targeted to ship in September 2021. 

### Who is behind it ?

Phyllome OS is currently a [one-man effort](https://refre.ch/home/), but couldn't exist without the work of thousands of open-source contributors.   

### Why use Fedora as a base for Phyllome OS ?

For a couple reasons :

* **Development velocity**
	* It would take much longuer to build a Linux-distribution from scratch, although it may eventually be necessary to do so to achieve Phyllome OS' vision. After all, Google [first used Ubuntu as a base for ChromeOS](https://en.wikipedia.org/wiki/Chrome_OS#History), then switched to Gentoo to finally build their own distribution. 

* **Piggy backing**
	* The kernel used by Fedora is fairly recent. It allows the project to benefit from new virtualization-related functionalities and extensive hardware support, including support for newer graphic cards and peripherals. 
  * Qubes OS' dom0 [is based on Fedora](https://www.qubes-os.org/doc/supported-versions/#dom0) : using Fedora for Phyllome OS means that it will be easier to implement security hardening techniques as developped by the Qubes OS team.
  * Fedora offers native support for Virgil 3D. 

* **Extensibility**
	* Fedora comes with a lot of packages, should the user want to extend Phyllome OS further. 

* **Sane security by default**
	* Fedora uses SELinux by default. 
  