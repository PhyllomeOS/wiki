---
title: Resize an existing virtual disk
description: 
published: true
date: 2024-07-13T13:33:59.560Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:41:29.087Z
---

# Resize a disk

## Background

A virtual machine's disk may have to be resized, typically due to lack of space. This page explains how to do so.

## Usage for Linux guests

> In-place expansion is not supported. A new disk of the desired size has to be created.
{.is-info}

* Navigate to the location that contains the existing image

```
cd /var/lib/libvirt/images
```

* Create a new blank disk image of the desired size

Use the following command to create a disk of 20 GB called `guest_20G.img`. 

```
qemu-img create -f raw guest_20G.img 20G
```

* Identify the filesystem layout of the existing disk `guest.img`

```
# virt-filesystems -a -l -h guest.img
Name       Type        VFS   Label  Size        Parent
/dev/vda1  filesystem  vfat  EFI    133935104   -
/dev/vda2  filesystem  ext4  boot   366869504   -
/dev/vda3  filesystem  ext4  root   9933475840  -
```

One can tell that the root partition is located under `/dev/vda3`. This is the one that will need to be expanded.

* Copy the formet old data to the new disk and expand the root partition of the said disk

> This command is cabable of expanding different kinds of filesystems, including `ext4` and `btrfs`  
{.is-info}

```
# virt-resize --expand /dev/vda3 guest.img guest_20G.img
``` 

* Review the changes

```
[   0.0] Examining guest_20G.img
**********

Summary of changes:

/dev/vda1: This partition will be left alone.

/dev/vda2: This partition will be left alone.

/dev/vda3: This partition will be resized from 10G to 20G.  The 
filesystem ext4 on /dev/vda3 will be expanded using the ‘resize2fs’ 
method.

**********
[   2.1] Setting up initial partition table on guest_20G.img
[  12.9] Copying /dev/vda1
[  13.1] Copying /dev/vda2
[  13.4] Copying /dev/vda3
 100% ⟦▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒⟧ 00:00
[  38.3] Expanding /dev/vda3 using the ‘resize2fs’ method

Resize operation completed with no errors.  Before deleting the old disk, 
carefully check that the resized disk boots and works correctly.
```

* Switch to the new disk for your virtual machine

Now that the new disk has been created, it can be used in the virtual machine.

```
# virsh edit guest
```

Locate the source line for the existing disk `guest.img`:

```
[...]
    <disk type='file' device='disk'>
      <driver name='qemu' type='raw' cache='writeback' discard='unmap'/>
      <source file='/var/lib/libvirt/images/guest.img'/>
      <target dev='vda' bus='virtio'/>
      <address type='pci' domain='0x0000' bus='0x04' slot='0x00' function='0x0'/>
    </disk>
[...]
```

Edit the said line so that it points to the new disk `guest-20G.img`:

```
[...]
    <disk type='file' device='disk'>
      <driver name='qemu' type='raw' cache='writeback' discard='unmap'/>
      <source file='/var/lib/libvirt/images/guest-20G.img'/>
      <target dev='vda' bus='virtio'/>
      <address type='pci' domain='0x0000' bus='0x04' slot='0x00' function='0x0'/>
    </disk>
[...]
```

Start the virtual machine and ensure that it is working properly. If it does, the former disk could be removed.

## Resources

As per the software description : "*qemu-img allows you to create, convert and modify images offline. It can handle all image formats supported by QEMU.*"

* Installation

On Fedora-related distributions, `virt-resize` is provided by the `guestfs-tools` package : 

```
# dnf install guestfs-tools
```

---

*[**Go to parent page**](https://wiki.phyllo.me/)*