---
title: Design
description: 
published: true
date: 2022-01-20T11:16:54.755Z
tags: 
editor: markdown
dateCreated: 2022-01-18T10:28:26.221Z
---

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
  
---

*[**Go to parent page**](/phyllomeos/)*