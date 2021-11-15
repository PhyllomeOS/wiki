---
title:  Checkbox your system
description: 
published: true
date: 2021-11-13T17:20:09.745Z
tags: 
editor: markdown
dateCreated: 2021-11-13T10:47:33.615Z
---

# Prepare the host computer

## Requirements

`To-do`

These instructions are valid for x86-64 computers that do ship with Linux or Windows

Phyllome OS targets x86 systems with hardware-assisted virtualization,
with a strong preference for those providing IOMMU as well. It may
support ARM[^49]- or RISC-V-based platforms in the future.

It is expected that Phyllome OS will consume approximately 1 CPU core
and 1 GB of RAM[^50], which should be enough to accommodate a few
virtual machines. For instance, on a system with a CPU with 4 cores and
8 GB of RAM, a guest virtual machine will be able to be assigned up to 3
cores and 7 GB of RAM.

### []{#anchor-43}Minimum requirements for Phyllome OS Desktop

-   x86 computer that supports the first generation of hardware-assisted
    virtualization extensions

    -   For AMD-based configurations, it means that AMD V is available
        and enabled
    -   For Intel-based configurations, it means that Intel VT-x is
        available and enabled

-   2-core processor

-   8 GB of RAM

-   SSD-based storage device to store disk images and Phyllome OS

-   Any graphics card (Linux or macOS guests only)

### []{#anchor-44}Recommended requirements for Phyllome OS Desktop

-   x86 computer that supports the second generation of
    hardware-assisted virtualization extensions

    -   For AMD-based configurations, it means that AMD Vi is available
        and enabled
    -   For Intel-based configurations, it means that Intel VT-d is
        available and enabled

-   8-core processor

-   16 GB of RAM

-   NVME-based storage device to store disk images and Phyllome OS

-   Two graphics cards or a graphics card that supports vfio-mdev or
    SR-IOV



## Enable IOMMU

### Access the firmware

### Modify the firmware configuration


*Now that you are done, you can go to the next section to [create an installation medium](/deploy/medium).*