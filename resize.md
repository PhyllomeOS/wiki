---
title: Resize a guest disk image
description: Resize a a guest disk image using qemu-img and virt-resize
published: true
date: 2021-09-12T08:28:18.891Z
tags: 
editor: markdown
dateCreated: 2021-08-12T10:55:58.877Z
---

# qemu-img and virt-resize

## Introduction

As per the software description : "*qemu-img allows you to create, convert and modify images offline. It can handle all image formats supported by QEMU.*"

Expanding a new disk implies creating a new blank image of the desired size and "copy" the existing disk into this new bigger image using virt-resize.

> In-place expansion is not supported.  
{.is-info}
 
## Installation

* On Fedora-related distributions, `virt-resize` is provided by the `guestfs-tools` package : 

```
# dnf install guestfs-tools
```

## Usage

* **Create a new disk image**

In-place expansion is not supported. A new disk of the desired size has to be created. 

Use the following command to create `phyllome_but_bigger.img`, a disk of 15 GiB 

```
$ qemu-img create -f raw phyllome-bigger.img 15G
```

* **Expand the root partition**

> This command only works if the root partition is located on vda3 and if the disk image filesystem uses EXT4.  
{.is-warning}

This command bellow requires root privileges. 

```
# virt-resize --expand /dev/vda3 phyllome.img phyllome_but_bigger.img

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

* **Inform your virtual machine to use the new disk**

*To-do*
