---
title: ReactOS reference
description: 
published: true
date: 2022-01-06T22:21:39.934Z
tags: 
editor: markdown
dateCreated: 2022-01-06T21:53:31.225Z
---

# ReactOS virtualization reference

## State of support

| **Hardware** | ReactOS 4.14 |
| :-- | -- |
| *Chipset* | i440fx only |
| *Firmware* | BIOS only but UEFI is under-way |
| *virtio-gpu* | No |
| *virtio-net* | **Yes** |
| *virtio-blk* | No |
| *virtio-scsi* | No |
| *virtio-keyboard* | No |
| *virtio-tablet* | No |

## Resources around virtualization and ReactOS

* Official resource on QEMU and ReactOS: https://reactos.org/wiki/QEMU
* Official supported hardware list: https://reactos.org/wiki/Supported_Hardware
* A Docker image for the ReactOS operating system: https://github.com/hectorm/docker-qemu-reactos
* Current effort to integrate ReactOS and QubesOS: https://github.com/QubesOS/qubes-issues/issues/2809
* GSoC 2018 idea to port more paravirtualized devices to ReactOS: https://reactos.org/wiki/Google_Summer_of_Code_2018_Ideas#Paravirtualization_Support