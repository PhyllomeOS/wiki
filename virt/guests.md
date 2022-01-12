---
title: Guests support
description: 
published: true
date: 2022-01-12T18:02:19.810Z
tags: 
editor: markdown
dateCreated: 2022-01-12T14:25:25.960Z
---

# Guests support matrix

> Support for guest systems differs widely. In general, free and open-source operating systems such as Linux distributions are better supported than proprietary operating systems.
{.is-info}

* The table bellow only show support for the latest operating systems.

| | Linux | Darwin | Windows |
| :- | :-: | :-: | :-: |
| *[Chipset](/virt/chipset)* | `i440fx` `Q35` | `Q35` | `i440fx` `Q35` |
| *[Platform Firmware](/virt/firmware)* | `SeaBIOS` `OVMF` `RHF` [^1] | `OVMF` | `SeaBIOS` `OVMF` `RHF` |
| *`virtio-gpu`* | **Yes** | No | No |
| *`virtio-video`* | Upcoming | No | **Yes** |
| *`virtio-snd`* | No | No | **Yes** |
| *`virtio-blk`* | **Yes** | **Yes** | **Yes** |
| *`virtio-scsi`* | **Yes** | **Yes** | **Yes** |
| *`virtio-fs`* | No | No | ? |
| *`virtio-net`* | **Yes** |  **Yes** | **Yes** |
| *`virtio-keyboard`* | No | No | ? |
| *`virtio-tablet`* | No | No | ? |

[^1]: RST stands for the Rust Hypervisor Firmware