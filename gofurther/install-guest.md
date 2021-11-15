---
title: Netboot for all
description: 
published: true
date: 2021-11-14T18:40:21.600Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:43:58.697Z
---

# Install a guest OS

## Forewords

As of now, `netboot.xyz` is the main way to install a guest operating system inside Phyllome OS. It is compatible with most (but not all) guest operating systems.

## Preparation

By default, `netboot.xyz.iso` should already be located under `var/lib/libvirt/iso`. If it's not the case, please use the following command to fetch it, or navigate to [the website](https://netboot.xyz/):

```
wget https://boot.netboot.xyz/ipxe/netboot.xyz.iso -P /var/lib/libvirt/iso/
```

## Create a virtual machine using `virt-install`

The command below will create a virtual machine without a disk.  

```
virt-install \
    --connect qemu:///system \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --name live-with-netboot-xyz \
    --boot uefi \
    --cpu host-model,topology.sockets=1,topology.cores=1,topology.threads=1 \
    --vcpus 1 \
    --memory 2048 \
    --video virtio \
    --channel spicevmc \
    --autoconsole none \
    --sound none \
    --controller type=virtio-serial \
    --controller type=usb,model=none \
    --controller type=scsi,model=virtio-scsi \
    --network network=default,model=virtio \
    --input type=keyboard,bus=virtio \
    --input type=tablet,bus=virtio \
    --rng /dev/urandom,model=virtio \
    --disk none \
    --cdrom=/var/lib/libvirt/iso/netboot.xyz.iso \
    --install no_install=yes
```

## Create a virtual machine using `virt-manager`

`to-be done`