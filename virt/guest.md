---
title: Guests support
description: 
published: true
date: 2022-01-20T11:11:16.478Z
tags: 
editor: markdown
dateCreated: 2022-01-12T14:25:25.960Z
---

# General guests support matrix

> Support for guest systems differs widely. In general, free and open-source operating systems such as Linux distributions are better supported than proprietary operating systems.
{.is-info}

* The table bellow only show support for the latest operating systems.

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

---

*[**Go to parent page**](/virt/)*