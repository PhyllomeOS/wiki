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

Phyllome OS is a Fedora Remix that will eventually inherit security measures in place in Fedora.

It also intends to bring some unique security-related features:

- Unprivileged virtual machines creation with `qemu:///session`, by default
- Filesystem-level encryption with `fscrypt`
- Minimal set of applications
- Unattended installation of security updates
- Alternative virtual machine monitors like the Cloud Hypervisor

## Features

### Data at-rest encryption

Currently, Phyllome OS does ***not*** provide any kind of encryption by default at the host level. 

For any virtual disks that will contain personal data, users are strongly advised to use full-disk encryption as provided by their guest operating system.

## Anti-features

### Graphic virtualization

Phyllome OS heavily relies on GPU or graphic virtualization, most notably through `virtio-gpu`, but also with `vfio-pci` or `vfio-mdev`. Granting a virtual machine 3D capabilities is not considered safe. Measures will be taken to reduce the risk, or at least to inform the user of potential security risks associated with certain techniques. 

---

*[**Go to parent page**](https://wiki.phyllo.me/)*