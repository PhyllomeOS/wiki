---
title: Choose
description: Understand if Phyllome OS is for you and pick the right version
published: true
date: 2021-11-12T13:51:50.058Z
tags: 
editor: markdown
dateCreated: 2021-11-11T18:18:23.807Z
---

# Is Phyllome OS right for you?

> Phyllome OS is still in its infancy and not yet ready for production use
{.is-warning}

Phyllome OS makes a few assumptions, including the following: 

* **Virtual machines have become viable personal computing environments, including for desktop computing** 
	* Due to their software-based nature, they are extremely flexible, and despite their nature, they can match or even exceed their physical counterparts abilities in some areas. 
* **The host operating system should not be modified, in general**
	* Two Phyllome OS hosts should barely differ, allowing virtual machines to be migrated from one host to the next.
  
Some limitations results directly from these choices.

## Limitations

Relying on a virtual machine as its primarily personal environment has key advantages, some as the ability to more easily migrate to a new host computer or the ability to create multiple virtual computers out of a single physical computer. However, it also comes with several limitations in comparison to using a bare-metal operating system. 

Some of these limitations will be tackled or greatly reduced one day, others might not. Let's list some of these. 

### Performance overhead

* Phyllome OS requires resources to run, resources that will not be accessible to guest operating systems.

### Suboptimal guest performance

* In most cases, running a virtual machine instead of using the physical hardware directly will come with a performance penalty. This penalty can be greatly reduced by using some techniques, such as letting the virtual machine access the underlying hardware directly, but this particular solution is by definition not scalable to multiple virtual machines.

### Limited features set

* Some operating systems are designed to leverage hardware features that may not be accessible to an operating system installed on a virtual machine, or that would require specific developments to be taken advantage of. 

### Increased general complexity

* Instead of running just an operating system on top of some physical hardware, any Phyllome OS user would need to manage it as well as their primarily guest operating system. As a result, it might be more difficult to troubleshoot an issue. 

### Decreased general usability

* Any physical device attached to a computer won't automatically be made to a guest virtual machine. For some users, it might be considered a hindrance. Phyllome OS relies on Linux drivers. Not all hardware fully supports Linux well, which may force users to rely on device or controllers passthrough. 

### Still undecided?

Here is a table to help you pick a **desktop-oriented** operating system. 

How to read this table? For instance: *If you care most about virtualization and security, you would be better off picking [Qubes OS](https://www.qubes-os.org/) or the upcoming [Spectrum](https://spectrum-os.org/) instead of Phyllome OS.*

|  | Security | Usability | 
|---|---|---| 
| *Virtualization* | [Qubes OS](https://www.qubes-os.org/) or [Spectrum](https://spectrum-os.org/) | **Phyllome OS Desktop** | 
| *Bare-metal* | [Sculpt](https://en.wikipedia.org/wiki/Genode#Sculpt) or [Fuchsia](https://en.wikipedia.org/wiki/Fuchsia_(operating_system)) | [Linux](https://en.wikipedia.org/wiki/List_of_Linux_distributions) or [BSD distro](https://en.wikipedia.org/wiki/List_of_BSD_operating_systems), [macOS](https://en.wikipedia.org/wiki/MacOS), [Windows](https://en.wikipedia.org/wiki/Microsoft_Windows) or [Chrome OS](https://en.wikipedia.org/wiki/Chrome_OS) | 

> In general, the vast majority of users will stick to the bottom-right corner of the table. 
{.is-info}

This table is not meant to be clear-cut. Phyllome OS is intended to be easy-to-use, but still isn't. Out of the box, Chrome OS [^1], or even Windows [^2], might be considered  more secure than most Linux desktop-oriented distributions [^3], at the price of greatly limiting user freedom and privacy, however. Due to their tight integration, some BSD distributions might be considered more secure than some Linux distributions. Finally, just as Phyllome OS, Qubes OS is compatible with running Windows-based guest systems. In other words, using virtualization, a user might be able to access more usable operating systems, and in the case of Phyllome OS, one may even host Qubes OS inside Phyllome OS.    

Please also note that macOS or Windows can also be used to host virtual machines, just as any Linux or BSD distributions.  

[^1]: See for instance the paper [*Security of Google Chromebook* (PDF)](http://dhanus.mit.edu/docs/ChromeOSSecurity.pdf) by Katherine Fang, Deborah Hanus, Yuzhi Zheng. 

[^2]: A common pain point for Linux security are desktop environments (DE), which have a limited user base scattered across many different DE: there is a lot of complexity due to adding desktop environments atop the Linux kernel and its associated tools. Simple bugs might still lurk in the codebase for a long time. See for instance [*Is the Linux desktop less secure than Windows 10: Or how super mario music can own your system* (PDF)](https://archive.fosdem.org/2017/schedule/event/linux_desktop_versus_windows10/attachments/slides/1730/export/events/attachments/linux_desktop_versus_windows10/slides/1730/fosdem_linux_desktop_security.pdf), by M.Hanno Böck (2017).

[^3]: Take for instance the boot process, or before an operating system effectively takes control over the hardware. Major operating systems editors that are working directly with OEM integrators have a distinct advantage over editors that aren't: they have almost unlimited resources and can tame the underlying hardware, effectively controlling, measuring and attesting the entire boot process. To implement a user-backed root of trust on a particular hardware platform, one would need to take several extra measures, relying on something like [Heads](https://github.com/osresearch/heads) which, among other things, involves physically flashing a more open firmware to a motherboard, a complicated process. Fortunately, some hardware integrators like [Purism](https://puri.sm/) or [System76](https://system76.com/) are backing security measures straight into hardware platforms while at the same time respecting user freedom. 

## Requirements

`To be fetched from white paper : hardware requirements ; Phyllome OS version`

## Use

Install

    From a live medium (default method)
    In a virtual machine (to hack it)
    From source




