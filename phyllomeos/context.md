---
title: Context
description: 
published: true
date: 2021-11-12T15:31:13.657Z
tags: 
editor: markdown
dateCreated: 2021-11-12T15:31:13.657Z
---

# []{#anchor-24}Phyllome OS

## []{#anchor-25}Context

### []{#anchor-26}Public clouds and open source software

Public clouds provide on-demand computing resources over the Internet.
The largest are called hyperscalers.

Almost all hyperscalers, at the notable exception of Microsoft Azure, ,
depend on open-source software[^19] to support their platform[^20]. Put
simply, without open-source software, they wouldn't exist, at least not
in their current form[^21].

In particular, the Linux operating system and its Kernel-based Virtual
Machine (KVM) module are two basic, essential, open-source building
blocks upon which these hyperscalers are built.

These providers also add their own custom software to the core engine
that propels their platform[^22]. Unfortunately, this custom software
remains for internal use only[^23].

Isn't there an equivalent to these custom building blocks available for
everyone to reuse ?

### []{#anchor-27}The rise of robust general-purpose hypervisors

Rust-vmm (or Rust-Virtual Machine Monitor) is an ongoing effort among
software and hardware companies, including some hyperscalers, to share
more of their codebase. Rust-vmm provides a platform to share reusable
virtualization-related code by means of Rust-crates[^24].

As of 2021, this project offers the closest open-source equivalent to
the aforementioned custom software used by hyperscalers.

At least three key projects using Linux and KVM are also taking
advantage of Rust-vmm :

-   crosvm (2010 --)

    -   Crosvm means the Chrome OS Virtual Machine Monitor. It allows
        the virtualization of guest systems on devices running Chrome OS
        and Chromium OS, its open-source counterpart. It is the oldest
        project of its kind, upon which others are built or forked.
    -   The ongoing Spectrum (2020) project is a promising attempt to
        built a secure desktop OS around Chromium OS, crosvm and the Nix
        declarative package management system.

-   firecracker (2018 --)

    -   Originally built for desktop systems, crosvm has also been
        reused as a foundation for firecracker, the serverless computing
        platform which powers AWS Lambda. This is a story not unlike
        that of KVM, which was originally built with desktop workloads
        in mind but later gained traction as a solution for other
        workloads.

-   Cloud Hypervisor (2019 --)

    -   Cloud Hypervisor may be considered as the spiritual successor to
        the now-defunct NEMU project. NEMU provided a stripped-down
        version of QEMU [^25].
    -   Contrary to crosvm and projects that rely on it, it is possible
        to run non-Linux virtual guest systems on Cloud Hypervisor,
        provided that they support UEFI.
    -   As of today, there is no desktop-oriented operating system
        intended to take advantage of Cloud Hypervisor.

  ----------------------------- -------- ------------- ------------------
                                crosvm   firecracker   Cloud Hypervisor
  QEMU                          No       No            No
  KVM                           Yes      Yes           Yes
  Desktop-friendly              Yes      No            No
  Support for non-Unix guests   No       No            Yes
  ----------------------------- -------- ------------- ------------------

Until recently, any attempt to create a local-first, free and
open-source operating system that could run atop affordable,
virtualization-friendly hardware[^26] using basic building blocks
similar to those used by major public clouds would rightfully be met
with skepticism.

Thanks to the rust-vmm umbrella project, assembling such an operating
system is now becoming a possibility.

## []{#anchor-28}Description

### []{#anchor-29}Phyllome OS

Phyllome OS intends to tap into some modern software- and
hardware-related innovations used in the cloud and make them available
to a wider audience locally: to bring some of the cloud back home, so to
speak, with a focus on performance and usability. As an operating
system, Phyllome OS makes it easier to run virtual machines locally
using off-the-shelf hardware : it is designed from the ground up to be
easy[^27]-and safe[^28]-to-use.

Technically speaking, Phyllome OS is an attempt to port the Cloud
Hypervisor to desktop systems[^29].

Conceptually, Phyllome OS can be thought of in several ways : as a
wrapper around operating systems that use a Graphical User Interface
(GUI), just as Docker is, among other things,a headless wrapper around
GUI-less containers ; as an abstraction between the hardware and the
operating system; as a local-first appliance or sandbox whose sole
purpose is to run general computing operating systems using
hardware-assisted virtualization, and hopefully run them well ; or as
just another attempt to bring Linux back to the desktop, albeit more
covertly this time.

As with popular existing operating systems, Phyllome OS is designed to
be installed on a single machine or host. Contrary to existing operating
systems, it abstracts the physical layer away, allowing diverse
operating systems to run concurrently on the same machine if the user so
desires.

### []{#anchor-30}The Phyllome OS Project

The Phyllome Project aims to build a community around open source
virtualization and to make the development of Phyllome OS sustainable.
The project relies on self-hosted open source software.