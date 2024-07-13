---
title: Resize an existing virtual disk
description: 
published: true
date: 2024-07-13T13:11:07.613Z
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

* Navigate to the location that contains the existing image.

```
cd /var/lib/libvirt/images
```

* Create a new blank disk image of the desired size

Use the following command to create a disk of 20 GB called `guest_20G.img`. 

```
qemu-img create -f raw guest_20G.img 20G
```

* Identify the filesystem layout of the existing disk




* Expand the root partition

> *This command expects the root partition to be located on the vda3 partition. It has only been tested against the `ext4`filesystem.*  
{.is-warning}

```
virt-resize --expand /dev/vda3 phyllome.img phyllome-bigger.img
``` 

* The following should appear

```
[   0.0] Examining phyllome.img
**********

Summary of changes:

/dev/vda1: This partition will be left alone.

/dev/vda2: This partition will be left alone.

/dev/vda3: This partition will be resized from 5G to 15G.  The 
filesystem ext4 on /dev/vda3 will be expanded using the ‘resize2fs’ 
method.

**********
[   2.1] Setting up initial partition table on phyllome-bigger.img
[  12.9] Copying /dev/vda1
[  13.1] Copying /dev/vda2
[  13.4] Copying /dev/vda3
 100% ⟦▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒⟧ 00:00
[  38.3] Expanding /dev/vda3 using the ‘resize2fs’ method

Resize operation completed with no errors.  Before deleting the old disk, 
carefully check that the resized disk boots and works correctly.
```

* *Switch to the new disk for your virtual machine*

*To-do*

## Resources

As per the software description : "*qemu-img allows you to create, convert and modify images offline. It can handle all image formats supported by QEMU.*"

* *Installation*

On Fedora-related distributions, `virt-resize` is provided by the `guestfs-tools` package : 

```
# dnf install guestfs-tools
```

---

*[**Go to parent page**](https://wiki.phyllo.me/)*