---
title: Security in Phyllome OS
description: 
published: true
date: 2022-01-31T13:00:59.353Z
tags: 
editor: markdown
dateCreated: 2022-01-31T12:35:54.544Z
---

# Security in Phyllome OS

> *Phyllome OS is currently in alpha stage. It should not be used to store any sensitive data*
{.is-warning}

Phyllome OS is a Fedora Remix and as such directly inherits every single security measures in place for Fedora-related distributions, such as SELinux. It also brings some unique security-related features.

* **Unique security-related features**
	* Unprivileged virtual machines with `qemu:///session`, by default
	* Filesystem-level encryption with `fscrypt`
  * Minimal sets of applications by default
* **Planned features**
	* Unattended installation of security updates
  * `systemd` hardening
  * `gnome-shell` hardening
  * The Cloud Hypervisor for `vfio-pci`

## Features

### Data at-rest encryption

Currently, Phyllome OS does **not** provide any kind of encryption by default at the host level. 

It provides early support for Filesystem-level encryption, which is just one line of defense. 

For any virtual disks that will contain personal data, users are strongly advised to use full-disk encryption as provided by their guest operating system.

## Anti-features

### Graphic virtualization

Phyllome OS heavily relies on GPU or graphic virtualization, most notably through `virtio-gpu`, but also with `vfio-pci` or `vfio-mdev`. Granting a virtual machine 3D capabilities is not considered safe. Measures will be taken to reduce the risk, or at least to inform the user of potential security risks associated with certain techniques. 

---

*[**Go to parent page**](https://wiki.phyllo.me/)*