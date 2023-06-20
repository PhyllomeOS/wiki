---
title: Firmware
description: 
published: true
date: 2022-01-25T21:56:41.651Z
tags: 
editor: markdown
dateCreated: 2022-01-25T14:50:10.751Z
---

# Platform firmware

Virtual devices, including virtual chipsets, are shipping alongside platform firmware. 

> ***Definition**: Firmware are software that are tightly integrated with the hardware. Almost every devices are shipping with some kind of firmware associated to it. For instance, motherboards include such programs, which in their case is tasked to properly boot hardware devices such as RAM modules, check their state and make them ready-to-use by an operating system*
{.is-info}

## Available platform firmware for virtual machines

### SeaBIOS

[SeaBIOS](https://www.seabios.org/SeaBIOS) is an implementation of a x86 BIOS which relies on [Coreboot](https://www.coreboot.org/) and can be used to boot virtual machines. It is incompatible with UEFI. It is also simpler.

### OVMF

[OVMF](https://github.com/tianocore/tianocore.github.io/wiki/OVMF), which stands for Open Virtual Machine Firmware, is a UEFI-compatible firmware. It is based on the larger [TianoCore](https://www.tianocore.org/) project, which provides an open-source implementation of a platform firmware that follows UEFI specifications. It is the default method to boot UEFI-based operating systems in a virtual machine.

### Rust Hypervisor Firmware

The [Rust Hypervisor Firmware](https://github.com/cloud-hypervisor/rust-hypervisor-firmware) (RHF) is a UEFI-compatible firmware. It is focused on simplicity and performance and is designed for virtual workloads. It is tightly integrated with the Cloud Hypervisor.

## Comparison

| | SeaBIOS | OVMF | RHF | 
| :-- | :-: | :-: | :-: |
| *BIOS* | **Yes** | No | No |
| *UEFI* | No | **Yes** | **Yes** |
| *Secureboot* | No | **Yes** | **Yes** |
| *Chipset support* | [`i440fx`](/virt/vm/chipset#i440fx) / [`Q35`](/virt/vm/chipset#q35) | [`i440fx`](/virt/vm/chipset#i440fx) / [`Q35`](/virt/vm/chipset#q35) | [`Q35`](/virt/vm/chipset#q35)? / [`virt`](/virt/vm/chipset#virt) | 
| *Guest support* | **Linux** / **Windows** | **Linux** / **Darwin** / **Windows** | **Linux** / **Windows** |
| *Virtual Function I/O (VFIO)* | No | Yes | Yes |

---

*[**Go to parent page**](https://wiki.phyllo.me/)*