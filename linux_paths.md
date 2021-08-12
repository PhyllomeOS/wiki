---
title: Virtualization paths on Linux
description: Some virtualization-related folders on a Linux-system
published: true
date: 2021-08-12T12:33:17.150Z
tags: 
editor: markdown
dateCreated: 2021-08-12T12:33:17.150Z
---

# Paths on Linux

This page lists where most of the stuff related to virtualization is located on a Linux operating system. This is based on Fedora. But it should be similar for other distributions.

## UEFI Firmware

* Default location for the x86-64 OVMF (UEFI) firmware

`/usr/share/edk2/ovmf/OVMF_CODE.fd`

* Default location for the x86-64 OVMF (UEFI) secureboot-enabled firmware

`/usr/share/edk2/ovmf/OVMF_CODE.secboot.fd`

### Nvram

* Default location of Nvram

`/var/lib/libvirt/qemu/nvram`

The Nvram contains the saved state of the UEFI configuration.

## Default location for disk images

* Any new virtual machines will be saved there :

`/var/lib/libvirt/images`