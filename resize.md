---
title: Resize a guest disk image
description: Resize a a guest disk image using qemu-img and virt-resize
published: true
date: 2021-08-12T10:55:58.877Z
tags: 
editor: markdown
dateCreated: 2021-08-12T10:55:58.877Z
---

# qemu-img

## Introduction

As per the software description : "*qemu-img allows you to create, convert and modify images offline. It can handle all image formats supported by QEMU.*"

Expanding a new disk implies creating a new blank image of the desired size and "copy" the existing disk into this new bigger image using virt-resize.

## Usage

* Create the new disk phyllome_but_bigger.img of the desired size. In this case, it is 15 GiB 

```
$ qemu-img create -f raw /var/lib/libvirt/images/phyllome_but_bigger.img 15G
```

* Expand the root partition on the disk. 

> This command only works if the root partition is located on vda3 and if the disk image filesystem uses EXT4.  
{.is-warning}

```
# virt-resize --expand /dev/vda3 phyllome.img phyllome_but_bigger.img
``` 

``` 
[   0.0] Examining phyllome.img
**********

Summary of changes:

/dev/sda1: This partition will be left alone.

/dev/sda2: This partition will be left alone.

/dev/sda3: This partition will be resized from 24.5G to 499.5G.  The 
filesystem ext4 on /dev/sda3 will be expanded using the ‘resize2fs’ 
method.

**********
[   2.1] Setting up initial partition table on nested-hypervisor-secure-boot.img
[  12.9] Copying /dev/sda1
[  13.1] Copying /dev/sda2
[  13.4] Copying /dev/sda3
 100% ⟦▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒⟧ 00:00
[  38.3] Expanding /dev/sda3 using the ‘resize2fs’ method

Resize operation completed with no errors.  Before deleting the old disk, 
carefully check that the resized disk boots and works correctly.
```

