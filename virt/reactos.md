---
title: ReactOS reference
description: 
published: true
date: 2022-01-06T22:56:15.812Z
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
| *virtio-net* | Yes |
| *virtio-blk* | No |
| *virtio-scsi* | No |
| *virtio-keyboard* | No |
| *virtio-tablet* | No |

## Resources around virtualization and ReactOS

* [Official resource on running ReactOS with QEMU](https://reactos.org/wiki/QEMU)
* [Hardware support list](https://reactos.org/wiki/Supported_Hardware) for ReactOS
* [Git repository](https://github.com/hectorm/docker-qemu-reactos) providing a Docker image for the ReactOS operating system
* [Current effort](https://github.com/QubesOS/qubes-issues/issues/2809) to integrate ReactOS and QubesOS
* [GSoC 2018 project idea](https://reactos.org/wiki/Google_Summer_of_Code_2018_Ideas#Paravirtualization_Support) to port more paravirtualized devices to ReactOS.