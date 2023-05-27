---
title: Roadmap
description: 
published: true
date: 2021-11-13T11:55:14.298Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:55:14.298Z
---

Below are the targeted features for the alpha version.

| | Phyllome OS alpha features |
| :- | :-: |
| *Nested-virtualization* | Yes |
| *Paravirtualization* | Full support on Linux guests |
| *IOMMU support* | Yes |
| *Migration* | Cold migration only |
| *Snapshots* | No |
| *Cloning* | Yes |
| *Virtual disks format* | RAW only |
| *PCI Passthrough* | Yes |
| *Sound* | PCI Passthrough |
| *Bluetooth* | PCI Passthrough |
| *USB* | PCI Passthrough |
| *Display modes* | Spice and VNC |
| *UEFI* | Yes |
| *Secure Boot* | Yes |
| *TPM* | Yes |

## Roadmap

| Fedora 34 | Phyllome OS alpha | Phyllome OS beta | Phyllome OS 1.0 |
| :- | :-: | :-: | :-: |
|Out-of-the box support for virtualization | No | Yes | Yes | Yes |
| Emulator/virtualizer | QEMU | QEMU | QEMU, Cloud Hypervisor | Cloud Hypervisor |
| Virtual chipset | i440fx / Q35 | Q35 | Q35, virt | virt |
| Firmware | OVMF, SeaBIOS | OVMF | OVMF | OVMF |
| Hypervisor | KVM | KVM | KVM | KVM |
| Based on | Itself | Fedora Server | Fedora Silverblue | Fedora Silverblue |
| Desktop-oriented | Possible | Yes | Yes | Yes |
| Package management | RPM | RPM | RPM-ostree | RPM-ostree |
| Rolling release | No | No | Yes | Yes |
| Live-edition | No | No | No | Yes |
| Local-first | Possible | Yes | Yes | Yes |
| Default filesystem | Btrfs | Ext4 | Ext4 | F2FS| 
| Host encryption | Possible | No | Filesystem-level encryption | Filesystem-level encryption | 
| GPU support | Intel, AMD and Nvidia | Intel | Intel and AMD | Intel, AMD and Nvidia |
| Target release date | Released | 2021 | 2022| 2022 |

### Beyond the first production-ready release

Here are some features that may be added later :

* **App store**
    * An application store for distributing prepackaged and easy-to-deploy operating systems
* **A new GUI application** to manage virtual machines
    * The virtual machine manager does more than what Phyllome OS needs. It would make sense to rely on a leaner, more simple
        software, similar to GNOME Boxes. 
    * Ideally, it would be written in Rust, just as the Cloud Hypervisor
* **Graphics**
    * Out-of-the box support for Single GPU passthrough
        * Support for single GPU passthrough would make it easier to run Phyllome OS on hardware that features a single graphics card lacking support for vfio-mdev.
   * Out-of-the box support for vfio-mdev on Nvidia, consumer grade GPUs.
        * A 2021 project is bringing vfio-mdev to Nvidia, consumer grade GPUs. It would be great to support it and offer Phyllome's users the ability to split their physical GPUs.
        * Out-of-the box support for SR/IOV on generation 11^th^ of Intel graphics
* **Streaming**
    * Making encoding and decoding a virtual machine desktop or display more efficient would allow for more diverse uses, including usable remote desktops.
        * For that to happen, it would mean to support virtio-video.
        * Another route would be to use WebRTC on Wayland.
* **Support the Virtual I/O Device (VIRTIO) Version 1.2**
    * Version 1.2 of the VIRTIO specification will soon be released with new virtual devices. Phyllome OS will need to support these.
* **Support platform-dependent confidential computing features**
    * On public clouds -- where many virtual machines are collocated underneath the same hypervisor -- there are ongoing efforts to
        make it possible to run workloads without having to blindly trust the host system. Some of those efforts rely on
        platform-specific technologies, such as Intel's SGX Secure Enclave or and AMD's Secure Encrypted Virtualization (SEV). It
        would be nice to be able to support these.
* **First-class support for more open x86 hardware**
    * It would be great to optimize Phyllome OS to work on a recent, more open x86 motherboard that supports both openBMC and
        Coreboot[^54].
* **Support beyond the x86 architecture**
    * Support for hardware based on ARM and RISC-V architectures would be great.

---

*[**Go to parent page**](https://wiki.phyllo.me/)*