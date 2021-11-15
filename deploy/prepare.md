---
title: Preparation
description: 
published: true
date: 2021-11-15T15:39:49.074Z
tags: 
editor: markdown
dateCreated: 2021-11-15T15:39:49.074Z
---

> Section under construction
{.is-warning}

# Prepare the host computer

## Requirements

These instructions are valid for x86-64 computers that do ship with Linux or Windows.

Phyllome OS targets x86 systems with hardware-assisted virtualization, with a strong preference for those providing IOMMU as well.

It is expected that Phyllome OS will consume approximately 1 CPU core and 1 GB of RAM, which should be enough to accommodate a few
virtual machines. For instance, on a system with a CPU with 4 cores and 8 GB of RAM, a guest virtual machine will be able to be assigned up to 3 cores and 7 GB of RAM.

### Minimum requirements for Phyllome OS Desktop

* x86 computer that supports the first generation of hardware-assisted virtualization extensions
    * For AMD-based configurations, it means that AMD V is available and enabled
    * For Intel-based configurations, it means that Intel VT-x is available and enabled
* 2-core processor
* 8 GB of RAM
* SSD-based storage device to store disk images and Phyllome OS
* Any graphics card (Linux or macOS guests only)

### Recommended requirements for Phyllome OS Desktop

* x86 computer that supports the second generation of hardware-assisted virtualization extensions
    * For AMD-based configurations, it means that AMD Vi is available and enabled
    * For Intel-based configurations, it means that Intel VT-d is available and enabled
* 8-core processor
* 16 GB of RAM
* NVME-based storage device to store disk images and Phyllome OS
* Two graphics cards or a graphics card that supports vfio-mdev or SR-IOV

## Enable IOMMU

### Access the firmware

During the boot process, you need to press a certain key to access the firmware configuration tool for your motherboard, also known as BIOS or UEFI. 

The most common keystrokes are <kbd>F2</kbd> or <kbd>Del</kbd>.

Hardware manufacturers could not agree on a common keystroke to access the firmware configuration tool, so please have a look at the documentation provided by your hardware manufacturer.

* **Windows-based computers**

`to be done`

### Modify the firmware configuration

`to be done`

### Make sure that hardware-assisted virtualization is enabled 

`to be done`

---