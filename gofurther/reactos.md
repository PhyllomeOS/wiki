---
title: ReactOS
description: 
published: true
date: 2022-01-06T18:15:20.929Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:52:33.257Z
---

# ReactOS 

[ReactOS](https://reactos.org/) is a open-source operating system meant to behave like Windows XP and Windows Server 2003.

In theory, it can run any software and work with any drivers developped for those closed-source operating systems. In practice, it is still under heavy-development and may not work as expected.

## Installation

> ReactOS is currently in **Alpha** stage and does **not** work with most virtio-devices.
{.is-warning}

### Download

* *Go fetch the latest build of the *Boot CD* version of ReactOS on the official website*: https://reactos.org/getbuilds/

* *Unzip it using p7zip* (`dnf install p7zip`).

```
7za x reactos-bootcd-0.4.15-dev-3628-ga6bf77e-x86-gcc-lin-dbg.7z
``` 

* *Copy the resulting ISO under* `/var/lib/libvirt/images`

```
mv reactos-bootcd-0.4.15-dev-3628-ga6bf77e-x86-gcc-lin-dbg /var/lib/libvirt/images
```

### Launch the installer

* *Clone the `legacy model` of virtual machine and, optionaly, rename it*

* *Add the ISO file you just downloaded and a 1GB IDE disk using the Virtual Machine Manager*

* *Power-on the virtual machine*

* *Connect to the console*




---

* Official resource https://reactos.org/wiki/QEMU


> It accepts donations: https://reactos.org/donate/

## State of support

| **Hardware** | ReactOS 4.14 |
| :-- | -- |
| *Chipset* | i440fx only |
| *Firmware* | BIOS only |
| *virtio-gpu* | No |
| *virtio-net* | **Yes** |
| *virtio-blk* | No |
| *virtio-scsi* | No |
| *virtio-keyboard* | No |
| *virtio-tablet* | No |
