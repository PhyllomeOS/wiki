---
title: Chipset
description: 
published: true
date: 2023-05-19T22:24:32.504Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:56:47.463Z
---

# Virtual chipsets

Just as physical computers, virtual machines are built around a central chipset. 

## Available chipsets for virtual machines

### i440fx

The `i440fx` virtual chipset is a legacy chipset, compatible with PCI.

### Q35

The `Q35` virtual chipset is based on a modern chipset, compatible with PCI-Express.

> Did you know that the Open Virtual Machine Firmware (OVMF), which is based on [TianoCore](https://www.tianocore.org/), is the default firmware for EFI-based virtual machines? Its configuration utility can be accessed using the <kbd>Esc</kbd> key.
{.is-info}

![uefi_tianocore_first-screen.png](/assets/tianocore/uefi_tianocore_first-screen.png)

*The TianoCore splash screen*

### virt

The `virt` virtual chipset is the most modern chipset, compatible with PCI-Express. It only supports [virtio-devices](/virt/vm/virtio).

## Comparison

|  | `i440fx` | `Q35` | `virt` |
| :- | :-: | :-: | :-: |
| *Firmware* | [SeaBIOS](/virt/vm/firmware#seabios) / [OVMF](/virt/vm/firmware#ovmf) | [SeaBIOS](/virt/vm/firmware#seabios) / [OVMF](/virt/vm/firmware#ovmf) | [OVMF](/virt/vm/firmware#ovmf) **?** / [RHF](/virt/vm/firmware#rust-hypervisor-firmware)  |
| *PS/2 devices* | **Yes** | **Yes** | No | 
| *USB Controller* | **Yes** | **Yes** | No | 
| *SATA Controller* | No | **Yes** | No |
| *IDE Controller* | **Yes** | No | No |
| *Floppy Controller* | **Yes** | No | No |
| *TPM Support* | No | **Yes** | No? |
| *PCI-Express Bus* | No | **Yes** | **Yes** |
| *PCI Bus* | **Yes** | No | No |
| *Virtual Function I/O* | No | **Yes** | **Yes** |

> The *`i440fx` and `Q35` chipsets are currently supported by Phyllome OS. Early support for the `virt` model is expected for the Beta version*
{.is-info}

## Resources

* [Official documentation](https://wiki.qemu.org/Features/Q35) on Q35 


---

*[**Go back to parent page**](/virt/vm)*