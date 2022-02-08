---
title: Context
description: 
published: true
date: 2022-02-08T20:56:54.325Z
tags: 
editor: markdown
dateCreated: 2021-11-12T15:31:13.657Z
---

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

Rust-vmm (or Rust-Virtual Machine Monitor) is an ongoing effort among software and hardware companies, including some hyperscalers, to share more of their codebase. Rust-vmm provides a platform to share reusable virtualization-related code by means of Rust-crates [^7].

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

---

*[**Go back to parent page**](/phyllomeos)*