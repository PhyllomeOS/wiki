---
title: Linux family
description: 
published: true
date: 2021-11-26T19:51:06.779Z
tags: 
editor: markdown
dateCreated: 2021-11-12T15:27:40.366Z
---

> Section under construction
{.is-warning}

# How to deploy common Linux systems

## Introduction

*virt-install* is a command-line utility to install virtual machines. 

### Prerequesites 

* These prerequesites are for Fedora only, as Phyllome OS ships with virt-install by default.

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

> Requires an Internet connection
{.is-info}

* Fetch a Fedora iso file using wget and put it in the current working directory

```
$ wget https://download.fedoraproject.org/pub/fedora/linux/releases/34/Server/x86_64/iso/Fedora-Server-dvd-x86_64-34-1.2.iso
```

* Fetch a kickstart script using wget and put it in the current working directory

```
$ wget https://git.phyllo.me/home/kickstart/raw/branch/main/leaves/imd.cfg 
```

> If using a custom kickstart script, make sure it includes the cdrom option.
{.is-warning}


* Deploy a UEFI-based machine with Fedora Server using the relative path of the local kickstart file

```
$ virt-install \
    --connect qemu:///system \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --name imd \
    --boot uefi \
    --cpu host-model,topology.sockets=1,topology.cores=2,topology.threads=2 \
    --vcpus 4 \
    --memory 8192 \
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
    --disk path=/var/lib/libvirt/images/imd.img,format=raw,bus=virtio,cache=writeback,size=5 \
    --location=/var/lib/libvirt/iso/Fedora-Server-dvd-x86_64-34-1.2.iso \
    --initrd-inject imd.cfg --extra-args "inst.ks=file:/imd.cfg"
```
### Remote installation with local kickstart

> Requires an Internet connection
{.is-info}

* Fetch a kickstart script using wget and put it in the current working directory

```
$ wget https://git.phyllo.me/home/kickstart/raw/branch/main/leaves/vmd.cfg 
```

> If using a custom kickstart script, make sure it includes repo information
{.is-warning}

```
$ virt-install \
    --connect qemu:///system \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --name vmd \
    --boot uefi \
    --cpu host-model,topology.sockets=1,topology.cores=2,topology.threads=2 \
    --vcpus 4 \
    --memory 8192 \
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
    --location=https://download.fedoraproject.org/pub/fedora/linux/releases/34/Everything/x86_64/os/ \
    --initrd-inject bmd.cfg --extra-args "inst.ks=file:/bmd.cfg"
```

### Remote installation with remote kickstart

* Alternatively, same as above but without fetching the kickstart file. The last line has to be swapped with : 

``` 
virt-install \
    --connect qemu:///session \
    --metadata description="Works with all GPUs on the host including Nvidia and does expect an EFI-based Linux guest" \
    --os-variant detect=off \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --name linux-egl-headless-gl \
    --boot uefi \
    --cpu host-model,topology.sockets=1,topology.cores=1,topology.threads=1 \
    --vcpus 1 \
    --memory 2048 \
    --video virtio \
    --graphics spice,listen=none \
    --graphics egl-headless,gl.enable=yes \
    --channel spicevmc \
    --channel unix,target.type=virtio,target.name=org.qemu.guest_agent.0 \
    --autoconsole none \
    --console pty,target.type=virtio \
    --sound none \
    --network type=user,model=virtio \
    --controller type=virtio-serial \
    --controller type=usb,model=none \
    --controller type=scsi,model=virtio-scsi \
    --input type=keyboard,bus=virtio \
    --input type=tablet,bus=virtio \
    --rng /dev/urandom,model=virtio \
    --disk path=/var/lib/libvirt/images/phyllome-desktop.img,format=raw,bus=virtio,cache=writeback,size=5 \
    --location=https://download.fedoraproject.org/pub/fedora/linux/releases/35/Everything/x86_64/os/ \
    --extra-args="inst.ks=https://raw.githubusercontent.com/PhyllomeOS/phyllomeos/main/leaves/phyllome-desktop.cfg"
```

### Local deployment without installation

The idea here is to define a virtual machine and use the netboot.xyz.iso as a way to boot into an installer. 

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

### Built-in unattended mode

virt-install can rely on libosinfo's unattended install support to deploy fedora34 without any user intervention:

`virt-install --install fedora32 --unattended`

### Cloud-init

Cloud-init may be used alongside virt-install:

`virt-install --install fedora34,cloud=yes --cloud-init root-password-generate=on ssh-key=/home/user/.ssh/test_rsa.pub disable=on`