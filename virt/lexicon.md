---
title: Lexicon
description: 
published: true
date: 2022-01-17T16:32:45.665Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:58:43.776Z
---

# Key terms related to virtualization 

## Emulator

Emulators or virtualizers are software that provide material components similar to physical hardware, but that are made of computer code instead of silicon, -- virtual hardware --, such as virtual floppy disks.

QEMU is a popular emulator that can act as a simulator or virtual machine monitor. In the latter case, it can leverage hardware acceleration,

## Hardware-assisted virtualization

Hardware-assisted virtualization is a feature of certain computer hardware made to take advantage of virtualization.

Such hardware reduces the overheads associated with virtualization and is thus key to unlocking near-native performance for virtual machines.

In other words, hardware-assisted virtualization translates into better performance for virtualized workloads, significantly reducing the gap in performance between a virtual machine and a physical one.

## Nested-virtualization

Nested-virtualization refers to the ability to run a virtual machine inside another virtual machine.

## Virtualization

Most computers are made of hardware and software. By analogy, the brain that animates the cells to control a body can be thought as the operating system that controls components of its body.

Virtualization can be defined as the ability to run a software-based computer inside a physical computer. It is a set of computer-related techniques that make it possible to create replicas of computer hardware out of computer code. Those replicas are often referred to as virtual
machines.

There are roughly three types of virtualization:

*   **Simulation or emulation**: when a computer is fully emulated and can be made to look like any device to an operating system
*   **Partition**: when computer resources are split such that each operating system can only see a subset of available hardware resources
*   **Paravirtualization**: when both hardware and software-assisted virtualization is being used. In this case, the guest is aware that     it is running in the virtualized environment, and acts accordingly.

Virtualization is used to better isolate resources on a physical computer and to distribute them across various workloads, enabling better use of resources through consolidation. For instance, with virtualization, multiple operating systems can run concurrently on a physical machine.

## Hypervisor

A hypervisor is an operating system or firmware that is designed to run guest systems: it handles scheduling, execution of hyper privileged instructions, memory management and over-commitment, and provides drivers for physical devices.

The Virtual Machine Monitor (VMM) is a software that runs on top of the hypervisor and manages the life cycle of a virtual machine. It provides device models for emulated devices and implements tasks such as start, suspend, migrate, and stop virtual machines.

The hypervisor and VMM work in tandem with emulators, which provide them virtual hardware.

As of 2021, there are two major open-source hypervisor that are both are able to leverage hardware-assisted virtualization:

-   Xen (2003)
-   Kernel-based Virtual Machine (KVM) module for Linux (2007)

## Device

Devices are computer components that can be attached to machines. They can be classified in two ways : physical or emulated.

| | Physical hardware | Emulated: model-based | Emulated: paravirtual |
| :- | :-: | :-: | :-: |
| *Design* | Specific | Specific | Generic |
| *Type* | Silicon-based  | Software-based | Software-based  |

*   **Physical**

    *   Physical components refer to devices that can be attached to a system. For instance, a dedicated physical graphics card attached to a physical system can be directly attached to a virtual machine, which then becomes responsible for managing it, a technique called *passthrough*. The PCI-SIG standards provide IOMMU-related specifications to allow a host operating system to not have a driver for a particular device and passthrough the device to the guest. The guest will have a device with nearly native performance, and use the standard vendor's drivers for the device.
    *   The PCI-SIG standards also provide a way to partition compatible devices using so-called Virtual Functions (VFs). In this case, the host manages the way a physical device is used by the guest. Both host and guest must have specific device drivers. It offers nearly native performance.

*   **Emulated**

    *   Model-based

        *   Model-based emulated hardware are designed after real devices, but are made out of computer code, not silicon. The i440fx and Q35 chipsets are both instances of emulated hardware. This is the slowest (but most compatible) way to provide a device to a guest. An emulated GPU is not going to be fast enough in an emulated mode to do 3D rendering.

    *   Paravirtual

        *   Paravirtual hardware, also known as paravirtualized Virtual I/O devices or simply virtio, are also made out of computer code. Contrary to emulated hardware, they function as a generic piece of software-based hardware which doesn't replicate a specific hardware component.

### Paravirtualization

Paravirtualization refers to the emulation practice of letting an operating system running in a virtualized environment know that it is running in such an environment.

Under this configuration, more efficient communication methods are available between the host and the guest, including VirtIO devices (e.g.: virtio-net for network devices, virtio-blk for block storage devices). Such devices can communicate directly with the host, instead of emulating every single command of an IDE, SATA, SCSI or NVMe device, as it is the case for model-based emulation.

### Virtual machine

A virtual machine is a recreation of a real, physical, silicon-based computer using software. It performs almost exactly as a physical computer, and can thus host an operating system.

The expression "virtual machine" is often abbreviated VM. VMs are also often referred to as guests, in contrast to the hosts that host them.

---

*[**Go back to parent page**](https://wiki.phyllo.me/phyllomeos)*