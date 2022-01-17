---
title: Limitations and advantages
description: 
published: true
date: 2022-01-17T15:33:39.501Z
tags: 
editor: markdown
dateCreated: 2022-01-07T10:28:18.542Z
---

# Limitations and advantages

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

---

***[Go to parent page](/phyllomeos)***