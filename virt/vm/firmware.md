---
title: Firmware
description: 
published: true
date: 2023-10-15T14:30:00.632Z
tags: 
editor: markdown
dateCreated: 2022-01-25T14:50:10.751Z
---

# Platform firmware

Virtual devices, including virtual chipsets, are shipping alongside platform firmware.

## Common platform firmware for virtual machines

### SeaBIOS

[SeaBIOS](https://www.seabios.org/SeaBIOS) is an implementation of an x86 BIOS which relies on [coreboot](https://www.coreboot.org/). It is used for legacy systems, but also to specialized and cloud optimized guests systems which don't require UEFI.

### OVMF

[OVMF](https://github.com/tianocore/tianocore.github.io/wiki/OVMF), which stands for Open Virtual Machine Firmware, is a UEFI-compatible firmware. 

It is based on the [TianoCore](https://www.tianocore.org/) project, which provides an open-source implementation of a platform firmware that follows UEFI specifications. 

It is the default method to boot UEFI-based operating systems in a virtual machine.

### Rust Hypervisor Firmware

The [Rust Hypervisor Firmware](https://github.com/cloud-hypervisor/rust-hypervisor-firmware) (RHF) is a UEFI-compatible firmware. It is focused on simplicity and performance and is designed to run cloud-centric operating systems. 

It is developed alongside the Cloud Hypervisor.

## Supported features

| | SeaBIOS | OVMF | RHF | 
| :-- | :-: | :-: | :-: |
| *BIOS* | **Yes** | No | No |
| *UEFI* | No | **Yes** | **Yes** |
| *Secure Boot* | No | **Yes** | ? |
| *Chipset* | [i440fx](/virt/vm/chipset#i440fx), [Q35](/virt/vm/chipset#q35) | [i440f](/virt/vm/chipset#i440fx), [Q35](/virt/vm/chipset#q35) | [virt](/virt/vm/chipset#virt) | 
| *Guests* | **Linux**, **Windows** | **Linux**, **Darwin**, **Windows** | **Linux**, **Windows** |
| *Virtual Function I/O (VFIO)* | No | **Yes** | **Yes** |

---

*[**Go to parent page**](https://wiki.phyllo.me/)*