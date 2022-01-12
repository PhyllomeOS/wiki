---
title: Chipset
description: 
published: true
date: 2022-01-12T13:33:26.097Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:56:47.463Z
---

# Virtual chipsets

## Description

> There are two kinds of virtual chipsets that are currently supported by Phyllome OS: `i440fx`, `Q35`. Eventually, the `virt` model will also be supported. 
{.is-info}

| **Support** | i440fx | Q35 | virt |
| :- | :-: | :-: | :-: |
| *PS/2 devices* | **Yes** | **Yes** | No | 
| *USB Controller* | **Yes** | **Yes** | ? | 
| *SATA Controller* | No | **Yes** | ? |
| *IDE Controller* | Yes | No | No |
| *Floppy Controller* | **Yes** | No | No |
| *TPM Support* | No | **Yes** | ? |
| *Firmware* | SeaBIOS OVMF | SeaBIOS OVMF | Rust firmware |
| *PCI-Express Bus* | No | **Yes** | **Yes** |
| *PCI Bus* | **Yes** | No | No |
| Virtual Function I/O | No | **Yes** | **Yes** |


## Dedicated page (upcoming)

> To be created and populated. It would be great to talk about these virtual chipsets versions (now there is the `Q35 6.1`). is there any breaking changes between revisions?
{.is-info}

* `i440fx`
* `Q35`
* `virt`

## Resources

* [Official documentation](https://wiki.qemu.org/Features/Q35) on Q35 