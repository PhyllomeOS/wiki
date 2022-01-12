---
title: ReactOS reference
description: 
published: true
date: 2022-01-12T14:47:42.749Z
tags: 
editor: markdown
dateCreated: 2022-01-06T21:53:31.225Z
---

# ReactOS reference

> The current state of support for ReactOS in Phyllome OS is poor
{.is-warning}

## State of support

> Porting new paravirtual devices to ReactOS would significantly improve the experience of running ReactOS inside Phyllome OS, and other virtualization solutions leveraging [paravirtual hardware](https://wiki.phyllo.me/e/en/virt/virtio). See [here](https://reactos.org/contributing/) on how you can contribute to ReactOS
{.is-info}

| **Hardware** | ReactOS 4.13 | ReactOS 4.14 |
| :-- | -- |
| *[Chipset](/virt/chipset)* | i440fx | i440fx |
| *[Firmware](/virt/firmware)* | SeaBIOS [^1] | SeaBIOS |
| *virtio-gpu* | No | No |
| *virtio-net* | No | **Yes** [^2] |
| *virtio-blk* | No | No |
| *virtio-scsi* | No | No |
| *virtio-fs* | No | No |
| *virtio-console* | No | No | 
| *virtio-keyboard* | No | No |
| *virtio-tablet* | No | No |

## Resources

* [Official resource](https://reactos.org/wiki/QEMU) on running ReactOS with QEMU
* [Hardware support list](https://reactos.org/wiki/Supported_Hardware) for ReactOS
* [Git repository](https://github.com/hectorm/docker-qemu-reactos) providing a Docker image for the ReactOS operating system
* [Current effort](https://github.com/QubesOS/qubes-issues/issues/2809) to integrate ReactOS and QubesOS
* [GSoC 2018 project idea](https://reactos.org/wiki/Google_Summer_of_Code_2018_Ideas#Paravirtualization_Support) to port more paravirtualized devices to ReactOS

## Footnotes

[^1]: Support for [UEFI](https://reactos.org/wiki/UEFI), and potentially OVMF, is under-way.
[^2]: See [here](https://doxygen.reactos.org/d1/dc8/virtio__types_8h.html#a5a27dcd221caab788e973f6964d84aa9) for the source code reference for `virtio-net` 