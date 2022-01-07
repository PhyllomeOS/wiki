---
title: Comparaison
description: 
published: true
date: 2022-01-07T11:13:31.045Z
tags: 
editor: markdown
dateCreated: 2022-01-07T10:39:15.878Z
---

# Comparaison

## Choosing a desktop-oriented OS

> This section might removed as it is confusing as of now. Phyllome OS is not really a replacement for bare-metal operating systems.
{.is-warning}

Here is a table to help you pick a **desktop-oriented** operating system. 

How to read this table? For instance: *If you care most about virtualization and put security first, you would be better off picking [Qubes OS](https://www.qubes-os.org/) or the upcoming [Spectrum](https://spectrum-os.org/) instead of Phyllome OS.*

|  | Security | Usability | 
|---|---|---| 
| *Virtualization* | [Qubes OS](https://www.qubes-os.org/) or [Spectrum](https://spectrum-os.org/) | **Phyllome OS Desktop** | 
| *Bare-metal* | [Sculpt](https://en.wikipedia.org/wiki/Genode#Sculpt) or [Fuchsia](https://en.wikipedia.org/wiki/Fuchsia_(operating_system)) | [Linux](https://en.wikipedia.org/wiki/List_of_Linux_distributions) or [BSD distro](https://en.wikipedia.org/wiki/List_of_BSD_operating_systems), [macOS](https://en.wikipedia.org/wiki/MacOS), [Windows](https://en.wikipedia.org/wiki/Microsoft_Windows) or [Chrome OS](https://en.wikipedia.org/wiki/Chrome_OS) | 

> In general, the vast majority of users will stick to the bottom-right corner of the table, because that is the operating system that ships preinstalled together with their hardware.
{.is-info}

This table is not meant to be clear-cut, or definitive. 

* For example, Phyllome OS is intended to be easy-to-use, but still isn't.
* Spectrum, which appears to be based on Chromium OS, might well end up being easier to use.
* Out of the box, Chrome OS [^1], or even Windows [^2], might be considered  more secure than most Linux desktop-oriented distributions [^3], at the price of greatly limiting user freedom and privacy, however. 
* Due to their tight integration, some BSDs distributions might be considered more secure than some Linux distributions. * People might find Windows easier to use than, say, Ubuntu. 
* Finally, just as Phyllome OS, Qubes OS is compatible with running Windows-based guest systems. In other words, using virtualization, a user might be able to access more usable operating systems, and in the case of Phyllome OS, one may even host Qubes OS inside Phyllome OS, for instance to test out Qubes OS.
* Also note that macOS or Windows can also be used to host virtual machines, just as any Linux or BSDs distributions. 

[^1]: See for instance the paper [*Security of Google Chromebook* (PDF)](http://dhanus.mit.edu/docs/ChromeOSSecurity.pdf) by Katherine Fang, Deborah Hanus, Yuzhi Zheng. 

[^2]: A common pain point for Linux security are desktop environments (DE), which have a limited user base scattered across many different DE: there is a lot of complexity due to adding desktop environments atop the Linux kernel and its associated tools. Simple bugs might still lurk in the codebase for a long time. See for instance [*Is the Linux desktop less secure than Windows 10: Or how super mario music can own your system* (PDF)](https://archive.fosdem.org/2017/schedule/event/linux_desktop_versus_windows10/attachments/slides/1730/export/events/attachments/linux_desktop_versus_windows10/slides/1730/fosdem_linux_desktop_security.pdf), by M.Hanno Böck (2017).

[^3]: Take for instance the boot process, or before an operating system effectively takes control over the hardware. Major operating systems editors that are working directly with OEM integrators have a distinct advantage over editors that aren't: these major editors have almost unlimited resources, sometimes almost perfect control over hardware, and can therefore tame the underlying hardware, effectively controlling, measuring and attesting the entire boot process. To implement a user-backed root of trust on a particular hardware platform, one would need to take several extra measures, relying on something like [Heads](https://github.com/osresearch/heads) which, among other things, involves physically flashing a more open firmware to a motherboard, a complicated process. Fortunately, some hardware integrators like [Purism](https://puri.sm/) or [System76](https://system76.com/) are backing security measures straight into hardware platforms, while at the same time respecting user freedom. 

> **Still undecided?** You can give Phyllome OS a try, as a live system booting off from a USB thumb drive, without impacting the existing operating system on your machine.

---

*[Go back one level](/phyllomeos/)*