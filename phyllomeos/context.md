---
title: Context
description: 
published: true
date: 2025-05-06T21:15:11.416Z
tags: 
editor: markdown
dateCreated: 2021-11-12T15:31:13.657Z
---

# What Phyllome OS is

Phyllome OS is a [Fedora Remix](https://fedoraproject.org/wiki/Remix) designed to leverage [hardware-assisted virtualization](https://wiki.phyllo.me/virt/lexicon#hardware-assisted-virtualization) and [paravirtualization](https://wiki.phyllo.me/virt/lexicon#paravirtualization) to make it easier to run virtualized operating systems locally.

# Context

## Public clouds and open source software

Public clouds provide on-demand computing resources over the Internet. The largest are called hyperscalers.

Almost all hyperscalers[^1], at the notable exception of Microsoft Azure, depend on open-source software[^2] to support their platform [^3]. Put simply, without open-source software, they wouldn't exist, at least not in their current form.[^4]

[^3]: In particular, the Linux operating system and its Kernel-based Virtual Machine (KVM) module are two basic, essential, open-source building blocks upon which these hyperscalers are built.

[^4]: Just as most of today’s computing landscape, a witty reader might add

[^1]: Nowadays, the majority of the cloud market is captured by Amazon and Microsoft. AWS runs on Xen, and Microsoft on Hyper-V which, incidentally, is very similar to Xen design-wise. Amazon is gradually shifting away  from Xen, but it will take a very long time for them to migrate to KVM. Microsoft, at least for now, is sticking with Hyper-V. Oracle Cloud used to be on Xen but is gradually migrating to KVM (Thanks to Pasha Tatashin for the summary). Some references: Google Cloud, Honig and Porter, “[7 Ways We Harden Our KVM Hypervisor at Google Cloud.](https://cloud.google.com/blog/products/gcp/7-ways-we-harden-our-kvm-hypervisor-at-google-cloud-security-in-plaintext/.)”; Alibaba Cloud, Zhang, “[KVM Forum 2017](https://kvmforum2017.sched.com/event/Bo16/kvm-performance-tuning-on-alibaba-cloud-yang-zhang-alibaba-cloud).” AWS, Hamilton, “[AWS Nitro System – Perspectives.](https://perspectives.mvdirona.com/2019/02/aws-nitro-system/)” In the comment section of his article, James Hamilton, one of the designers of the new AWS Nitro System which powers EC2 instances on AWS, explains : “The Nitro hypervisor is built on a minimized and modified Linux kernel, including the KVM subsystem that is responsible for programming hardware virtualization features of the processor.”

[^2]: Open-source or free software are software that are freely available to the general public to reuse, read and modify.

These providers also add their own custom software to the core engine that propels their platform [^5]. Unfortunately, this custom software remains for internal use only[^6].

[^5]: For instance, Google Cloud does not rely on QEMU. In an attempt to reduce the attack surface of the platform, its designers decided to replace QEMU – which by default comes with a vast amount of generic features – with their own specialized user-space emulator, which is rumored to be called Vanadium. According to the [Wikipedia article](https://en.wikipedia.org/wiki/Vanadium), Vanadium as as physical compound “is a hard, silvery-grey, malleable transition metal [...] rarely found in nature [...] [O]nce isolated artificially, the formation of an oxide layer [...] somewhat stabilizes the free metal against further oxidation.” *Vanadium would surely be a fitting name for a user-space emulator*...

[^6]: he fact that the hyperscalers’ foundations are closed source has several key consequences which go beyond the issues that Phyllome OS seeks to address. Individuals, private companies, and public entities increasingly rely on public clouds to run their most critical workloads. The core engine that propels those hyperscalers is made of computer code that no external party can audit, which means that the aforementioned critical workloads are ultimately not auditable. In other words, individuals, private companies and public entities are building their own essential digital infrastructures on top of black boxes.

*Isn't there an equivalent to these custom building blocks available for everyone to reuse?*

## The rise of robust general-purpose hypervisors

[Rust-vmm](https://github.com/rust-vmm/community) (or Rust-Virtual Machine Monitor) is an ongoing effort among software and hardware companies, including some hyperscalers, to share more of their codebase. Rust-vmm provides a platform to share reusable virtualization-related code by means of Rust-crates [^7].

[^7]: Crates are snippets of Rust code which provide certain functions or sets of functions.

As of 2021, this project offers the closest open-source equivalent to the aforementioned custom software used by hyperscalers.

At least three key projects using Linux and KVM are also taking advantage of Rust-vmm :

* **crosvm** (2010 --)
    * Crosvm means the Chrome OS Virtual Machine Monitor. It allows the virtualization of guest systems on devices running Chrome OS and Chromium OS, its open-source counterpart. It is the oldest project of its kind, upon which others are built or forked.
    * The ongoing Spectrum (2020) project is a promising attempt to built a secure desktop OS around Chromium OS, crosvm and the Nix declarative package management system.

* **firecracker** (2018 --)
    * Originally built for desktop systems, crosvm has also been reused as a foundation for firecracker, the serverless computing platform which powers AWS Lambda. This is a story not unlike that of KVM, which was originally built with desktop workloads in mind but later gained traction as a solution for other workloads.

* **Cloud Hypervisor** (2019 --)
    * Cloud Hypervisor may be considered as the spiritual successor to the now-defunct [NEMU project](https://github.com/intel/nemu). NEMU provided a stripped-down version of QEMU.
    * Contrary to crosvm and projects that rely on it, it is possible to run non-Linux virtual guest systems on Cloud Hypervisor, provided that they support UEFI. 
    * As of today, there is no desktop-oriented operating system intended to take advantage of Cloud Hypervisor.

| | crosvm | firecracker | Cloud Hypervisor |
| :- | :-: | :-: | :-: |
| *QEMU* | No | No | No |
| *KVM* | **Yes** | **Yes** | **Yes** |
| *Desktop-oriented* | **Yes** | No | No |
| *Support for non-Unix guests* | No | No | **Yes** |

Until recently, any attempt to create a local-first, free and open-source operating system that could run atop affordable, virtualization-friendly hardware[^8] using basic building blocks similar to those used by major public clouds would rightfully be met with skepticism.

[^8]: Hyperscalers tend to rely more on custom-made hardware, which might significantly raise the entry bar for new competitors in the future

Thanks to the rust-vmm umbrella project, assembling such an operating system is now becoming a possibility.

Phyllome OS intends to tap into some modern software- and hardware-related innovations used in the cloud and make them available to a wider audience locally: to bring some of the cloud back home, so to speak.

## Comparaison

Phyllome OS draws inspiration from numerous other projects, including desktop-oriented systems such as [Qubes OS](https://www.qubes-os.org/), [Tails](https://tails.boum.org/), and [Fedora Silverblue](https://silverblue.fedoraproject.org/), as well as others specialized in running container workloads, such as [Fedora CoreOS](https://silverblue.fedoraproject.org/) and [RancherOS](https://rancher.com/).

When it comes to virtualization-friendly, open-source, desktop-oriented operating systems, two projects stand out: Qubes OS and [Spectrum](https://spectrum-os.org/). How do they compare to Phyllome OS?

## Qubes OS

Like Phyllome OS, Qubes OS is based on Fedora but relies on Xen, the other popular open-source hypervisor for Linux. 

Xen strongly isolates components of the hardware stack, including the USB and network controllers. By design, it works in parallel rather than alongside Linux, as KVM does. KVM’s more tight integration with the Linux Kernel can be considered an advantage or a disadvantage.

Out of security concerns, Qubes OS does not yet support 3D-accelerated virtual machines, even though its parent project Xen does support this functionality. Phyllome OS intends to support 3D acceleration inside virtual machines, even if it means increasing the attack surface.

## Spectrum

Just as with Qubes OS, Spectrum’s main focus is secure computing. Spectrum uses Nix, a declarative packet manager. It is built atop crosvm and thus doesn’t rely on QEMU, largely reducing the attack surface. Through a re-implementation of the virtio-wayland device, which is used in Chrome OS to securely run Linux apps alongside the main OS, Spectrum will eventually allow its guests’ virtual machines to have a GPU capable of efficiently accelerating 3D applications.

By design, Spectrum won't support operating systems that don't rely on the Wayland protocol.

|  | Qubes OS | Spectrum | Phyllome OS 1.0 | 
| :- | :-: | :-: | :-: |
| *Emulator* | QEMU[^1] | crosvm | Cloud Hypervisor |
| *Hypervisor* | Xen | KVM | KVM |
| *Virtual chipset* | i440fx? / Q35? | ? | virt |
| *Default filesystem* | Ext4? | Ext4? | F2F2 |
| *Non-Linux guests support* | Yes | No | Yes |
| *Based on* | Fedora | Chromium OS? | Fedora CoreOS |
| *Desktop Environment* | Xfce | Aura? | GNOME Shell/Headless|
| *Package management* | RPM | Nix | RPM-ostree |
| *Rolling release* | No | Yes? | Yes |
| *Live edition* | No | No | Yes |
| *OS as the center of the UX* | Yes | Yes | No |
| *Portability of VMs* | No | No | Yes |
| *Security-focused* | yes | yes | no |
| *Encryption* | [dm-crypt](https://www.kernel.org/doc/html/latest/admin-guide/device-mapper/dm-crypt.html) | [dm-crypt](https://www.kernel.org/doc/html/latest/admin-guide/device-mapper/dm-crypt.html) | [fscrypt](https://www.kernel.org/doc/html/v4.18/filesystems/fscrypt.html) |


[^1]: Since 2017, Xen, upon which Qubes OS relies, is also exploring the possibility to [avoid using QEMU](https://wiki.xenproject.org/wiki/Xen_Project_Software_Overview#Guest_Types) for guests using hardware-assisted virtualization. See the diagram on the “Guest Types” section:“Xen Project Software Official Overview.”.

From a design perspective, Qubes OS and Spectrum are end-to-end operating systems, whereas Phyllome OS is only a wrapper around the user’s preferred operating system. Thanks to nested-virtualization, it could even be used to host those operating systems, but in this configuration, the attack surface would be significantly increased, and the performance would take a significant hit, especially for nested guests.

In Phyllome OS, the main computing activity will happen inside the user’s virtual machine. In QubesOS, Dom0 (“domain zero”) is at the center of the user’s experience. 

In summary, despite some shared characteristics, Phyllome OS is not meant to be a replacement for Qubes OS or Spectrum, but could become a test bed for these operating systems.

---

*[**Go to parent page**](https://wiki.phyllo.me/)*