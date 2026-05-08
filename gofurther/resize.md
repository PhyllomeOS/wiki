---
title: Resize an existing virtual disk
description: 
published: true
date: 2026-05-08T09:34:59.946Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:41:29.087Z
---

# Resize a virtual disk

## Background

A virtual machine's disk may have to be resized, typically due to lack of space. This page explains how to do so.


## Preparation 

### Shut down virtual machine

> Please ensure that the virtual machine using the virtual disk to be resized is turned off
{.is-warning}

Let's assume that you wish to increase the size of the virtual machine called *guest*.

- List virtual machines running on your host

```
# virsh list --all

Id   Name                                State
----------------------------------------------------
 1    guest                              running
```

- Shutdown the *guest* virtual machine

```
# virsh shutdown guest
```

- Ensure that the virtual machine is fully shut off

```
# virsh list --all

Id   Name                                State
----------------------------------------------------
 1    guest                              shut off
```

It is now safe to proceed to the next step

### Backup existing disk

It is advisable to make a backup first.

- Navigate to the correct directory

```
# cd /var/lib/libvirt/images
```

- Make a copy of the virtual disk image

```
# cp guest.img backup_guest.img
```

## Linux guests


> In-place expansion is not supported. A new disk of the desired size has to be created, and then swap with the former disk.
{.is-info}

- Navigate to the location that contains the existing image

```
# cd /var/lib/libvirt/images
```

- Create a new blank 20 GB disk called `guest_20G.img`

```
# qemu-img create -f raw guest_20G.img 20G
```

- Identify the filesystem layout of the existing disk `guest.img`, which is ext4-based

```
# virt-filesystems -a guest.img -l -h
Name       Type        VFS   Label  Size        Parent
/dev/vda1  filesystem  vfat  EFI    1.3G        -
/dev/vda2  filesystem  ext4  boot   3.6G        -
/dev/vda3  filesystem  ext4  root   10G         -
```

- Another output for a btrfs-based filesystem

```
# virt-filesystems -a bazzite-desktop.img -l -h
Name                    Type       VFS   Label         Size Parent
/dev/sda1               filesystem vfat  -             599M -
/dev/sda2               filesystem ext4  bazzite_xboot 1.9G -
/dev/sda3               filesystem btrfs bazzite       37G  -
btrfsvol:/dev/sda3/root filesystem btrfs bazzite       -    -
btrfsvol:/dev/sda3/home filesystem btrfs bazzite       -    -
btrfsvol:/dev/sda3/var  filesystem btrfs bazzite       -    -
```

Thanks to the label on the ext4-based based image, one can tell that the root partition is `/dev/vda3`. This is the one that will need to be expanded. For the btrfs example, the root partition `/dev/sda3`as shown by `btrfsvol:/dev/sda3/root`

* Copy the former old data to the new disk and expand the root partition of the said disk

> This command is capable of expanding different kinds of filesystems, including `ext4` and `btrfs`  
{.is-info}

The command takes the new empty disk as last argument. 

> Data could be erased if you mix argument!
{.is-warning}
```
# virt-resize --expand /dev/vda3 guest.img guest_20G.img
``` 

* Review changes

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