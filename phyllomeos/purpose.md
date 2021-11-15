---
title: Purpose
description: 
published: true
date: 2021-11-12T15:31:30.659Z
tags: 
editor: markdown
dateCreated: 2021-11-12T15:31:30.659Z
---

## Purpose

Why would one prefers to use an operating system installed on virtual hardware ?

Adding a layer of abstraction between the operating system and the virtualization-friendly hardware allows for support of newer operating systems, beyond what the physical hardware can support.

* By using Phyllome OS on Apple hardware that do not support the latest iteration of macOS, one could create a virtual machine and install the latest iteration of macOS anyway, further extending the life of hardware.
    * **Note:** Phyllome OS does not and will **not** support running macOS on anything but Apple hardware, as it is -- sadly -- not allowed by Apple.
    * Windows 11 requires a Trusted Platform Module (TPM). By using a virtual machine alongside a virtual TPM on unsupported hardware, one could still run Windows 11. The passthrough of a real TPM may also be supported.

### Advantages

More generally, a software-based/backed computer, or simply a virtual machine, has many advantages over a silicon-based computer :

* **Cost** : the cost of creating a virtual machine tends to zero
* **Flexibility** : a software-backed computer, alongside its operating system, can be migrated to new physical hosts. In other
    words, when a user acquires a new physical computer, the entire computing environment may be copy/pasted to the new machine.
-   **Compatibility** : contrary to silicon-based computers, which tend to be optimized to work at most with only a handful operating
    systems, a virtual machine can be designed to work with most operating systems.

### Limitations

Alas, it also comes with limitations, including but not limited to :

* Limited out-of-the box hardware support : hardware-assisted virtualization is available on many computers but rarely activated by default and not always correctly implemented. Users remain a the mercy of good platform firmware and may have to explicitly activate hardware-assisted virtualization in the BIOS/UEFI. Hardware components are often not correctly isolated in IOMMU groups.
    * Offering first-class support for only a handful of curated computers might provide an answer, at the price of compatibility. 
    * When it comes to IOMMU groups, a workaround might have to be used for models that do not offer well-isolated IOMMU groups, a workaround that has security implications.

* Reliance on devices or controllers passthrough to cover edge cases: virtual hardware do not cover all features a user may expect to have, including out of the box support for Bluetooth, wireless, or sound adapters. For those cases, USB or PCI Passthrough might be used.
    * Again, offering first-class support for only a handful of curated computers might provide an answer, at the price of compatibility.
    * New virtual hardware are expected, including paravirtualized sound cards, which will improve the situation.
