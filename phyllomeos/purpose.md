---
title: Purpose
description: 
published: true
date: 2022-02-09T20:19:32.002Z
tags: 
editor: markdown
dateCreated: 2021-11-12T15:31:30.659Z
---

# Phyllome OS in a nutshell

The goal of Phyllome OS is to make it possible to run most operating systems locally on most hardware.

## Problematic

Most PC hardware is designed to work with a single operating system. Since the beginning, the end-users' freedom is serverly restricted, as the operating system is almost always preinstalled.[^1] Isn’t there a way to allow users to run their favorite operating system on most hardware?

[^1]: Popular and proprietary operating systems such as macOS Big Sur or Windows 11 are optimized to only run on a limited set of computers. This state of affairs significantly limits users’ choice and may incite them to renew their hardware frequently, as operating systems providers may decide to drop support for older hardware models for any number of reasons.

[Virtualization](/virt/lexicon#virtualization) provides a partial answer to this question as it allows the abstraction of the underlying hardware, presenting generic software-based hardware to the operating system. In other words, by means of virtualization, a specific physical computer can be partially abstraced away and made to look generic to an operating system.

To be compatible with physical hardware, including USB controllers or graphic cards, one would still need to use a base operating system that can provide software to drive these physical devices.[^3] Most Linux distributions, including Fedora or Debian, ship with a large selection of such drivers, and as such represent another part of the solution to this problem.[^4] 

[^4]: The industry is even developing drivers for Linux first, at least for certain categories of components such as Network Interface Cards (NICs).

[^3]: An operating system must possess drivers to allow it to interact with hardware components, devices or peripherals such as storage controllers, graphic cards or keyboards. Each driver has to be specifically written to work with a particular operating system. A specific piece of hardware requires a specific driver tailored for each operating systems out there. Achieving support across operating systems is an almost insurmountable task as there are dozen unique operating systems out there.

## In summary 

The idea behind Phyllome OS is to rely on Linux to provide drivers for specific hardware components and virtualization[^5] to provide a limited set of generic virtualized hardware that are already or could be made to work with most operating systems. The burden of hardware compatibility is put on Linux, freeing the operating system underneath, which would only need to provide generic virtual hardware drivers[^2].

[^5]: There are many types of virtualization. Phyllome OS is primarily focused on paravirtualization, which assumes that an operating system running in a virtualized environment is aware of being virtualized. For any operating systems to run well in such an environment, one would only have to focus on developing and maintaining a set of generic drivers for virtual hardware, a task that is well under way for many popular operating systems, including Linux-based, Darwin-based or Windows NT-based operating systems.

[^2]: For instance, to provide storage block capacity, a developer of a specific operating system like Sculpt OS or ReactOS would only need to develop support for virtio-blk for its environment, and resort to Linux to interact with the hardware directly.

Technically speaking, Phyllome OS is an operating system, a free and open source Linux distribution, a Fedora Remix based on Fedora Server designed to leverage hardware-assisted virtualization to run graphically-accelerated UNIX and non-UNIX-based operating systems locally, in a virtual machine, using off-the-shelf hardware and open source software.

## Commandments

Phyllome OS tries to stick to three generic rules or commandments, which can be summed up as follows : Phyllome OS should stay out of users’ way and allow them to run their current operating system well.

* **Stay out of my way**
	* Users shouldn’t have to spend much time managing Phyllome OS.

* **Run my current operating system**[^1]
 	* Phyllome OS is designed to be the coziest home for a user’s favorite operating system36, not a replacement for it. Users should be able to continue to use their preferred operating system.

[^1]: Such compatible guests include Linux, Windows NT and Darwin-based OS.

* **Run it well**
	* Most users will only want to run one, or at most a handful of, virtual machines  concurrently [^2], just as most users only use one machine at a time. Phyllome OS should attempt to maximize the performance of the virtual machine it hosts, with the goal of matching its physical counterpart.
  
[^2]: Of course, power-users will be able to run as many systems as their hardware allows.

# Design decisions

* **Provide a user-friendly interface**
	* The first iteration of Phyllome OS will ship with a stripped-down GNOME-based shell, `libvirt` – a powerful and almost ubiquitous virtualization API – and the virtual machine manager software. Having a full-feature desktop environment will allow users to switch more easily between virtual machines and to fall back to a friendly environment whenever they shut down their virtual machine. A headless version of Phyllome OS will  eventually be released.
  
* **Just enough applications by default, only the necessary software**
	* Phyllome OS is meant to be distraction-free, which means that it will only ship with applications required to satisfy its main purpose: run modern virtual machines.
  
* **Favor generic virtual hardware, use passthrough at a last resort**
	* Phyllome OS is about making your personal computing environment less reliant on the hardware you currently use to host it. As a result, it will favor virtual hardware and especially paravirtualized hardware (virtio) over real hardware passthrough. Hardware passthrough is considered an anti-pattern, as it requires users to make sure that the operating system a device is being passthroughed to does actually support the device.
  
* **Read-only whenever possible**
	* Phyllome OS is not made to be heavily modifiable on run-time.
  * Two Phyllome OS hosts using the same version should barely differ, allowing a user to easily migrate their virtual machines to compatible hosts.
  
* **Encrypt virtual disks by default**
	* Phyllome OS will rely on fscrypt to encrypt virtual disks at rest.
  
* **Minimize user generated-data storage**
	* Phyllome OS should avoid touching user-generated data or storing it. In general, it is not meant as a place for the user to do computing.
  
* **Be compatible with proprietary operating systems**
	* hyllome OS strongly favors virtual machines running free software and will support running Linux systems natively, with the widest number of features and virtual devices. Alas, on the desktop, the vast majority of users still rely on proprietary operating systems. Phyllome OS will do its best to take into account the needs of those users too, and to offer a good experience with virtualization.

## Limitations and advantages

There are multiple reasons one would want to rely on virtual machines extensively, or even exclusively, an approach championed by Phyllome OS. Let's list some significant advantages of this approach, but also cover severe limitations.

### Advantages

A software-based/backed computer, or simply a virtual machine, has many advantages over a silicon-based computer:

* **Cost**: the cost of creating a virtual machine tends to zero. Virtual machines are made of computer code, and it is basically free to copy or to duplicate them.
* **Flexibility**: a software-backed computer, alongside its operating system, can be migrated to new physical hosts. In other words, when a user acquires a new physical computer, the entire computing environment may be copy/pasted to the new machine.
* **Compatibility**: contrary to silicon-based computers, which tend to be optimized to work at most with only a handful operating systems, a virtual machine can be designed to work with most operating systems.
* **Support**: Adding a layer of abstraction between the operating system and the virtualization-friendly hardware allows for support of newer operating systems, beyond what the physical hardware can support. Windows 11 requires a Trusted Platform Module (TPM) to be present. By using a virtual machine alongside a virtual TPM on unsupported hardware, one could still run Windows 11.
* **Flexibility**. Due to their software-based nature, virtual machines are extremely flexible, and can for instance emulate features that their physical host may lack (i.e.: a [TPM](https://en.wikipedia.org/wiki/Trusted_Platform_Module); an extra network card). 

### Limitations

Relying on a virtual machine as its primarily personal environment comes with several limitations in comparison to using an operating system installed on the hardware (aka known as bare-metal computing). Some of these limitations will be tackled or greatly mitigate one day, others might not.

* **Performance overhead**. Phyllome OS requires resources to run, resources that will not be accessible to guest operating systems.
	* *Running Phyllome OS, headless, without a desktop environment, might help to mitigate this issue at the price of usability.*
  * *Further optimizations will be made to reduce the memory footprint of Phyllome OS, such as identifying unnecessary services and stopping them.*

* **Suboptimal guest performance**. In most cases, running a virtual machine instead of using the physical hardware directly will come with a performance penalty.
	* *This penalty can be greatly reduced by using some techniques, such as letting the virtual machine access the underlying hardware directly. However, this particular solution is by definition not scalable to multiple virtual machines.*

* **Limited out-of-the box hardware support**: hardware-assisted virtualization is available on many computers, but rarely activated by default and not always correctly implemented. Users remain at the mercy of good platform firmware and may have to explicitly activate hardware-assisted virtualization in the BIOS/UEFI. Hardware components are often not correctly isolated in IOMMU groups.
    * Offering first-class support for only a handful of curated computers might provide an answer, at the price of compatibility. 
    * When it comes to IOMMU groups, a workaround might have to be used for models that do not offer well-isolated IOMMU groups, a workaround that has security implications.

* **Limited features set**. Some operating systems are designed to leverage hardware features that may not be accessible to an operating system installed on a virtual machine, or that would require specific developments to be taken advantage of (i.e: a Bluetooth dongle; a [Near-field communication chip](https://en.wikipedia.org/wiki/Near-field_communication); etc.)

* **Increased general complexity**. Instead of running just an operating system on top of some physical hardware, any Phyllome OS user would need to manage it as well as their primarily guest operating system. As a result, it might be more difficult to troubleshoot an issue, and it will add a pile of code that the user has to trust.

* **Decreased general usability**. Any physical device attached to a computer won't automatically be made to a guest virtual machine. For some users, it might be considered a hindrance. Phyllome OS relies on Linux drivers. Not all hardware fully supports Linux well, which may force users to rely on device or controllers passthrough. Finally, the use of Phyllome OS will certainly greatly reduce a laptop's battery-life over running a single system. 

* **Lack of guest systems' integration**. Phyllome OS provides an optimized virtual machine model tuned to host modern operating systems, but, at the exception of some RPM-based guests operating systems including Phyllome OS itself, does not intent to provide automated ways to deploy guest operating systems (at the moment, [Infrastructure as code solutions](https://en.wikipedia.org/wiki/Infrastructure_as_code) or instance initialization software like [cloud-init](https://github.com/canonical/cloud-init) do not seem generic enough to satisfy every modern desktop-based operating systems' idiosyncrasies). In other words, contrary to end-to-end operating systems like [Qubes OS](https://www.qubes-os.org/) or the upcoming [Spectrum](https://spectrum-os.org/), which are offering ready to use templates or/and applications isolated in virtual machines by default, Phyllome OS delegates to end-users the task to install their favorite operating system, while trying to provide the best possible underlying defaults for each operating system. In this regard, its model is closer to [Proxmox](https://www.proxmox.com/en/), which doesn't make assumptions about how a guest operating system will be deployed.

## Use cases

* **Run multiple guest operating systems concurrently**
	* Plug in two screens, two sets of keyboards, and two mice to the same PC and spawn two machines to do graphic intensive tasks such as gaming or 3D modeling. No need to buy another computer, just split the one you already have.

* **Painlessly move to new hardware**
	* When virtualized, your operating system is just a file on Phyllome OS' disk. You can move and restore it on another computer, provided that the targeted host runs Phyllome OS.

* **Make your current hardware last longer**
	* Most recent versions of modern operating systems require recent hardware to function, and may not work on otherwise perfectly functioning hardware. By providing modern virtual hardware, Phyllome OS allows users to receive operating system updates, despite the fact that their underlying may not officially be supported.

* **Go beyond what your physical hardware is capable of**
	* A virtual display in a virtual machine can be set to a resolution that exceeds what the underling physical display is capable of, and such a virtual display may be accessible remotely, over the network. 

---

*[**Go to parent page**](https://wiki.phyllo.me/)*