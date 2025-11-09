---
title: Firmware
description: 
published: true
date: 2025-11-08T10:28:07.779Z
tags: 
editor: markdown
dateCreated: 2022-01-25T14:50:10.751Z
---

# Platform firmware

Virtual devices, including virtual chipsets, are shipping alongside platform firmware.

## SeaBIOS

[SeaBIOS](https://www.seabios.org/SeaBIOS) is an implementation of an x86 BIOS which relies on [coreboot](https://www.coreboot.org/). It is used for legacy systems, but also to specialized and cloud optimized guests systems which don't require UEFI.

## OVMF

[OVMF](https://github.com/tianocore/tianocore.github.io/wiki/OVMF), which stands for Open Virtual Machine Firmware, is a UEFI-compatible firmware. 

It is based on the [TianoCore](https://www.tianocore.org/) project, which provides an open-source implementation of a platform firmware that follows UEFI specifications. 

It is the default method to boot UEFI-based operating systems in a virtual machine, and ddoes not support Compatibility Support Module (CSM). A virtual machine booting x86 BIOS won't be able to boot with OVMF.

Under Fedora-based systems such as Phyllome, firmware that can be used by virtual machines are stored in the following directory `/usr/share/edk2/ovmf`


| Name | Description | 
| :-- | :--: |
| OVMF_CODE.fd | 2MB default OVMF firmware. Used by default |
| OVMF_VARS.fd | Variables store |
| OVMF_CODE.secboot.fd  | 2MB firmware with secure boot enabled |
| OVMF_VARS.secboot.fd | Firmware variables with secure boot enabled |
| OVMF_CODE.secboot.pcrlock | Firmware with secure boot and [PCR locking](https://www.freedesktop.org/software/systemd/man/257/systemd-pcrlock.html) |
| OVMF_CODE_4M.qcow2 | 4MB firmware in qcow2 format for virtualization |
| OVMF_VARS_4M.qcow2 | 4MB variable store in qcow2 format for virtualization |
| OVMF_CODE_4M.secboot.pcrlock | 4MB firmware with secure boot and PCR locking |
| OVMF_CODE_4M.secboot.qcow2 | 4MB firmware with secure boot in qcow2 format |
| OVMF_VARS_4M.secboot.qcow2 | 4MB variable store with secure boot in qcow2 format |
| OVMF_CODE.cc.fd | Firmware code with confidential computing support |
| OVMF.qemuvars.fd | QEMU-specific firmware variables |
| OVMF.stateless.fd | Stateless firmware without persistent storage |
| OVMF.stateless.secboot.fd | Stateless firmware with secure boot |
| OVMF.stateless.secboot.pcrlock | Stateless firmware with secure boot and PCR locking |
| OVMF.amdsev.fd | [AMD SEV](https://docs.kernel.org/virt/kvm/x86/amd-memory-encryption.html) (Secure Encrypted Virtualization) support. Allow the memory contents of a VM to be transparently encrypted with a key unique to that VM |
| OVMF.igvm | Firmware with [IGVM loader](https://github.com/roy-hopkins/buildigvm). To be used alongside SEV platforms |
| OVMF.inteltdx.fd | [Intel Trust Domain Extensions](https://en.wikipedia.org/wiki/Trust_Domain_Extensions) (TDX) support |
| OVMF.inteltdx.secboot.fd | TDX with secure boot support |

### Resources :

- [OVMF 2015 whitepaper](https://www.linux-kvm.org/downloads/lersek/ovmf-whitepaper-c770f8c.txt)

## Rust Hypervisor Firmware

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