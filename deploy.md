---
title: Automatic deployment of a Fedora guest
description: Deploy a Fedora automatically with virt-install
published: true
date: 2021-08-12T14:41:09.641Z
tags: 
editor: markdown
dateCreated: 2021-08-12T10:06:58.917Z
---

# Virt-install

## Introduction

*virt-install* is a command-line utility to install virtual machines.

### Installation

Install the *virt-install* command-line tool on Fedora :

```
# dnf install virt-install
```

## Manual installation

Use the following command to automatically launch the Fedora installation process. It will also automatically create a disk image to install Fedora on. Make sure you have at least 20 GB of free space.

```
$ virt-install --install fedora32

Using fedora32 --location https://download.fedoraproject.org/pub/fedora/linux/releases/32/Everything/x86_64/os
Using default --name fedora32
Using fedora32 default --memory 2048
Using fedora32 default --disk size=20

Starting install...
Retrieving file vmlinuz...                                                                             |  10 MB  00:00:00     
Retrieving file initrd.img...                                                                          |  74 MB  00:00:03     
Allocating 'fedora32-2.qcow2'                                                                          |  20 GB  00:00:00     
Running graphical console command: virt-viewer --connect qemu:///session --wait fedora32
```

It should automatically launch the guest console. Eventually, you should see the Anaconda installer first page.

Other options include : `android-x86-9.0`, `centos8`, `clearlinux`, `debian9`, `macosx10.7`, `nixos-20.03`, `ubuntu20.04`, `win10`


> The virt-install package that comes with Fedora 34 doesn't work yet with argument *fedora34*
{.is-warning}

## Automated installation 

### Local iso and kickstart

* Fetch a Fedora iso file

```
$ wget https://download.fedoraproject.org/pub/fedora/linux/releases/34/Server/x86_64/iso/Fedora-Server-dvd-x86_64-34-1.2.iso -P /var/lib/libvirt/iso 
```

* Deploy a Fedora Server using Phyllome OS curated kickstart

```
$ virt-install \
    --connect qemu:///system \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --name vmd \
    --boot uefi \
    --cpu host-model,topology.sockets=1,topology.cores=1,topology.threads=2 \
    --vcpus 2 \
    --memory 4096 \
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
    --disk path=/var/lib/libvirt/images/vmd.img,format=raw,bus=virtio,cache=writeback,size=5 \
    --location=/var/lib/libvirt/iso/Fedora-Server-dvd-x86_64-34-1.2.iso \
    --extra-args="inst.ks=https://git.phyllo.me/home/kickstart/raw/branch/master/leaves/vmd.cfg"
```

> Requires an Internet connection
{.is-info}


### Built-in unattended mode

virt-install can rely on libosinfo's unattended install support to deploy fedora34 any user intervention:

`virt-install --install fedora32 --unattended`

### Cloud-init

Cloud-init may be used alongside virt-install:

`virt-install --install fedora34,cloud=yes --cloud-init root-password-generate=on ssh-key=/home/user/.ssh/test_rsa.pub disable=on`