---
title: Limitations and advantages
description: 
published: true
date: 2022-01-07T10:28:44.474Z
tags: 
editor: markdown
dateCreated: 2022-01-07T10:28:18.542Z
---

# Limitations and advantages

## Assumptions

Phyllome OS makes a few assumptions, including the following ones: 

* **Virtual machines are performant enough to host personal computing environments**
* **Phyllome OS, the host operating system, should not be modified post-deployment**
	* Two Phyllome OS hosts should barely differ, allowing virtual machines to be migrated from one host to the next.

### Limitations

Relying on a virtual machine as its primarily personal environment comes with several limitations in comparison to using an operating system installed on the hardware (aka known as bare-metal computing). Some of these limitations will be tackled or greatly mitigate one day, others might not.

* **Performance overhead**. Phyllome OS requires resources to run, resources that will not be accessible to guest operating systems.
	* *Running Phyllome OS, headless, without a desktop environment, might help to mitigate this issue at the price of usability.*
  * *Further optimizations will be made to reduce the memory footprint of Phyllome OS, such as identifying unnecessary services and stopping them.*

* **Suboptimal guest performance**. In most cases, running a virtual machine instead of using the physical hardware directly will come with a performance penalty.
	* *This penalty can be greatly reduced by using some techniques, such as letting the virtual machine access the underlying hardware directly. However, this particular solution is by definition not scalable to multiple virtual machines.*

* **Limited features set**. Some operating systems are designed to leverage hardware features that may not be accessible to an operating system installed on a virtual machine, or that would require specific developments to be taken advantage of (i.e: a Bluetooth dongle; a [Near-field communication chip](https://en.wikipedia.org/wiki/Near-field_communication); etc)

* **Increased general complexity**. Instead of running just an operating system on top of some physical hardware, any Phyllome OS user would need to manage it as well as their primarily guest operating system. As a result, it might be more difficult to troubleshoot an issue, and it will add a pile of code that the user has to trust.

* **Decreased general usability**. Any physical device attached to a computer won't automatically be made to a guest virtual machine. For some users, it might be considered a hindrance. Phyllome OS relies on Linux drivers. Not all hardware fully supports Linux well, which may force users to rely on device or controllers passthrough. Finally, the use of Phyllome OS will certainly greatly reduce a laptop's battery-life over running a single system. 

* **Lack of guest systems' integration**. Phyllome OS provides an optimized virtual machine model tuned to host modern operating systems, but, at the exception to some RPM-based guests operating systems including Phyllome OS itself, does not intent to provide automated ways to deploy guest operating systems (at the moment [Infrastructure as code solutions](https://en.wikipedia.org/wiki/Infrastructure_as_code) or instance initialization software like [cloud-init](https://github.com/canonical/cloud-init) do not seem generic enough to satisfy every modern desktop-based operating systems' idiosyncrasies). In other words, contrary to end-to-end operating systems like [Qubes OS](https://www.qubes-os.org/) or the upcoming [Spectrum](https://spectrum-os.org/), which are offering ready to use templates or/and applications isolated in virtual machines by default, Phyllome OS delegates to end-users the task to install their favorite operating system, while trying to provide the best possible underlying defaults for each operating system. In this regard, its model is closer to [Proxmox](https://www.proxmox.com/en/), which doesn't make assumptions about how a guest operating system will be deployed.

### Advantages

* **Flexibility**. Due to their software-based nature, virtual machines are extremely flexible, and can for instance emulate features that their physical host may lack (i.e.: a [TPM](https://en.wikipedia.org/wiki/Trusted_Platform_Module); an extra network card). 

* **Hardware independence**. One can migrate its personal computing environment to a new host computer. 

... *To be continued*

---

*[Go back one level](/phyllomeos/)*