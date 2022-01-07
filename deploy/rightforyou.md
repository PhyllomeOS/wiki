---
title: Understand what you are signing up for
description: 
published: true
date: 2022-01-07T10:51:52.896Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:19:38.215Z
---

# Is Phyllome OS right for you?

## Understand the Phyllome OS philosophy

> *Phyllome OS has one goal: to let users bring their favorite operating system and to run them well. Eventually, users should be able to reach **the state of virtual enlightenment** (tm), and stop worrying about the fact that their favorite operating system is running inside a virtual machine, just as humans should stop worrying about living in a computer simulation* ([perhaps?](https://en.wikipedia.org/wiki/Simulation_hypothesis)).

By definition, the host, Phyllome OS, is trying to be as discrete as possible, so that users won't actually have to spend much time to manage it. Users should be able to spend their time using their favorite personal computing environment, rather than messing around with Phyllome OS itself. Although, we very much encourage you to [hack it](https://github.com/PhyllomeOS/phyllomeos#how-to-hack-phyllome-os).

However, if the host is meant to be a great place for guest operating systems to thrive, it is up to the user to manage the lifecycle of their guest operating system. Phyllome OS provides an optimized virtual machine model tuned to host modern operating systems, but, at the exception of some RPM-based guests operating systems including Phyllome OS itself, does not intent to provide automated ways to deploy guest operating systems (at the moment [Infrastructure as code solutions](https://en.wikipedia.org/wiki/Infrastructure_as_code) or instance initialization software like [cloud-init](https://github.com/canonical/cloud-init) do not seem generic enough to satisfy every modern desktop-based operating systems' idiosyncrasies).

In other words, contrary to end-to-end operating systems like [Qubes OS](https://www.qubes-os.org/) or the upcoming [Spectrum](https://spectrum-os.org/), which are offering ready to use templates or/and applications isolated in virtual machines by default, Phyllome OS delegates to end-users the task to install their favorite operating system, while trying to provide the best possible underlying defaults for each operating system. In this regard, its model is closer to [Proxmox](https://www.proxmox.com/en/), which doesn't make assumptions about how a guest operating system will be deployed.

## Assomptions

Phyllome OS makes a few assumptions, including the following ones: 

* **Virtual machines have become viable personal computing environments, including for desktop computing** 
	* Due to their software-based nature, virtual machines are extremely flexible, and can for instance emulate features that their physical host may lack. 
* **The host operating system should not be modified, in general**
	* Two Phyllome OS hosts should barely differ, allowing virtual machines to be migrated from one host to the next.

## Limitations

Some limitations directly result from these assumptions.

Relying on a virtual machine as its primarily personal environment has key advantages, such as the ability to more easily migrate to a new host computer or the ability to create multiple virtual computers out of a single physical computer. However, it also comes with several limitations in comparison to using a bare-metal operating system.  Some of these limitations will be tackled or greatly reduced one day, others might not.

### Performance-related

* **Performance overhead**. Phyllome OS requires resources to run, resources that will not be accessible to guest operating systems.

* **Suboptimal guest performance**. In most cases, running a virtual machine instead of using the physical hardware directly will come with a performance penalty. This penalty can be greatly reduced by using some techniques, such as letting the virtual machine access the underlying hardware directly, but this particular solution is by definition not scalable to multiple virtual machines.

### Usability-related

* **Limited features set**. Some operating systems are designed to leverage hardware features that may not be accessible to an operating system installed on a virtual machine, or that would require specific developments to be taken advantage of. 

* **Increased general complexity**. Instead of running just an operating system on top of some physical hardware, any Phyllome OS user would need to manage it as well as their primarily guest operating system. As a result, it might be more difficult to troubleshoot an issue, and it will add a pile of code that the user has to trust.

* **Decreased general usability**. Any physical device attached to a computer won't automatically be made to a guest virtual machine. For some users, it might be considered a hindrance. Phyllome OS relies on Linux drivers. Not all hardware fully supports Linux well, which may force users to rely on device or controllers passthrough. Finally, the use of Phyllome OS will severely reduce your laptop battery-life. 

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

