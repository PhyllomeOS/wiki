---
title: Guests support
description: 
published: true
date: 2022-01-20T11:42:37.903Z
tags: 
editor: markdown
dateCreated: 2022-01-12T14:25:25.960Z
---

# Guest operating system

> *Phyllome OS 🤎 other operating systems. It is meant to be a cozy platform for almost any modern operating systems to thrive.*

Although Phyllome OS would like to support as many operating systems as possible, due to limited resources and the intent to be forward compatible with the Cloud Hypervisor, it will mainly focus on modern, UEFI-compatible operating systems that are shipping with support for `virtio` devices.

## Support matrix

> *Support for guest systems differs widely. In general, free and open-source operating systems such as Linux distributions are better supported than proprietary operating systems*.
{.is-info}

* The table below only show support for the latest operating systems.

| | Linux | Darwin | Windows |
| :- | :-: | :-: | :-: |
| *[Chipset](/virt/chipset)* | `i440fx` `Q35` `virt` | `Q35` | `i440fx` `Q35` `virt` |
| *[Platform Firmware](/virt/firmware)* | `SeaBIOS` `OVMF` `RHF` [^1] | `OVMF` | `SeaBIOS` `OVMF` `RHF` |
| *`virtio-gpu`* | **Yes** | No | No |
| *`virtio-video`* | *Upcoming* | No | No |
| *`virtio-snd`* | *Upcoming* | No | No |
| *`virtio-blk`* | **Yes** | **Yes** | **Yes** |
| *`virtio-scsi`* | **Yes** | No | **Yes** |
| *`virtio-fs`* | **Yes** | No | **Yes** |
| *`virtio-net`* | **Yes** |  **Yes** | **Yes** |
| *`virtio-keyboard`* | **Yes** | No | **Yes** |
| *`virtio-tablet`* | **Yes** | No | **Yes** |

[^1]: RHF stands for the Rust Hypervisor Firmware

## Resource

* **Distrowatch**: 
	* [All active operating systems and Linux distributions](https://distrowatch.com/search.php?ostype=All&category=All&origin=All&basedon=All&notbasedon=None&desktop=All&architecture=All&package=All&rolling=All&isosize=All&netinstall=All&language=All&defaultinit=All&status=Active#simple) listed on Distrowatch
	* [List of other operating systems awaiting validation](https://distrowatch.com/dwres.php?resource=links#new), still on Distrowatch
* **OSDev.org**
	* [OSDev.org](https://wiki.osdev.org/Main_Page), a great place to learn about Operating System Development.
	* [List of active operating systems](https://wiki.osdev.org/Projects) on OSDev.org
  
---

*[**Go to parent page**](/virt/)*