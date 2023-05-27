---
title:  A very short history of virtualization
description: 
published: true
date: 2022-01-18T09:35:02.581Z
tags: 
editor: markdown
dateCreated: 2022-01-17T20:30:10.094Z
---

#  A very short history of virtualization

## The prehistory of virtualization

Virtualization[^1] as a computer-related technology is rather old: its foundations date back as early as the 60s[^2]. 

[^1]: When we refer to virtualization, we talk about full virtualization, also known as machine, system or platform-level virtualization (i.e. virtual machines or guest systems), not operating-system virtualization (i.e. containers).

[^2]: See for instance a “[Timeline of Virtualization Development.](https://en.wikipedia.org/wiki/Timeline_of_virtualization_development)” on Wikipedia

At that time, computers generally weren’t available outside of the academia or other well-funded circles.

## The rise of personal computing

For many countries, the democratization of general purpose and personal computers happened between the 80s and the 90s.

At that time, many architectures and operating systems were in competition with one another. At the turn of the millennium, however, a consolidation happened: computers based on the x86 instruction set architecture came to dominate the consumer market[^3].

[^3]: In the 1990s, Intel was, and still is, as of 2021, the main provider of x86-based CPUs. AMD comes in distant second.

## Hardware-assisted virtualization

In 2005, a new set of specialized CPU features for the x86 architecture was introduced, providing hardware-assisted virtualization[^4].

[^4]: Intel Virtualization, abbreviated Intel VT-x, first appeared in 2005. AMD Virtualization, abbreviated AMD-V, was introduced in 2010, and is similar to its Intel counterpart. It was originally referred to as AMD SVM, for Secure Virtual Machine.

This may be considered the first generation of virtualization-specific features for the x86 architecture.

This first generation of CPU features specific to virtualization was followed just before 2010s by the introduction of another set of features, which pushed the technology further, implementing a so-called Input–Output Memory Management Unit (IOMMU) for virtualization[^5].

[^5]: Intel Virtualization Technology for Directed I/O, abbreviated Intel VT-d, was first introduced in 2011. AMD I/O Virtualization Technology, abbreviated AMD-Vi, was also introduced in 2011, and is similar to its Intel counterpart. They are both IOMMU-based.

Through IOMMU, which is available for other architectures as well, guest machines can access the physical hardware directly and in a safer way, significantly reducing the overhead  for most workloads while retaining certain security properties. 

In summary, the second generation of virtualization-specific CPU technologies for the x86 architecture improved the performance as well as the security of running virtualized workloads[^6].

[^6]: Although IOMMU only provides security and performance benefits if a device is being passthroughed, it  also provides security enhancements for the host in general if configured correctly.

## The commodification of hardware-assisted virtualization

For hardware-assisted virtualization to be useful to the general public, it would still need to be widely available, which means that most CPUs and platforms would have to be supported, regardless of the market segment they target: low to high-end, consumer- or professional-grade hardware.

In this regard, the latter part of 2010 marks a turning point, at least when it comes to the first generation of CPU extensions: general-purpose hardware-assisted virtualization is now widely available in most – if not all – x86-based computing hardware sold to the public[^7].

[^7]: Most recent ARM64-based chips also support hardware-assisted virtualization.

As of 2021, the year in which this paper is being written, the commodification of hardware-assisted virtualization is already well underway. 

Alas, affordable and widely accessible hardware is only one part of the answer. Just as with any other CPU extensions, to be useful and widely accessible, software that are designed to take advantage of hardware-assisted virtualization should exist and be accessible to the masses.

## Open-source virtualization

On common Linux distributions, virtualization is often driven by the KVM/QEMU or the Xen/QEMU duo. 

With this software stack deployed on virtualization-friendly hardware, an operating system running on a virtual machine can be become almost indistinguishable from an operating system running on a physical computer.

## Timeline from the 2000s

* 2003 : Xen
* 2005? : QEMU
* 2005 : First generation of hardware-assisted virtualization (x86)
* 2007 : KVM
* ~2009 : Second generation of hardware-assisted virtualization (x86, IOMMU-based)
* 2015 : Commodification of hardware-assisted virtualization (x86)

---

*[**Go to parent page**](https://wiki.phyllo.me/)*