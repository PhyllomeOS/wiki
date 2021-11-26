---
title: Linux family
description: 
published: true
date: 2021-11-26T20:40:46.772Z
tags: 
editor: markdown
dateCreated: 2021-11-12T15:27:40.366Z
---

# Deploy common Linux systems automatically

`virt-install` is a command-line utility that can be used to create virtual machines. It is preinstalled on Phyllome OS. 

* For Fedora, you can install it using the following command:

```
# dnf install virt-install
```

## Automated installation using an ISO file and a local kickstart

> Requires an Internet connection
{.is-info}

* Fetch a Fedora ISO file using wget and put it in the current working directory

```
$ wget https://download.fedoraproject.org/pub/fedora/linux/releases/34/Server/x86_64/iso/Fedora-Server-dvd-x86_64-34-1.2.iso
```

* Fetch a kickstart script using wget and put it in the current working directory

```
$ wget https://git.phyllo.me/home/kickstart/raw/branch/main/leaves/imd.cfg 
```

> If using a custom kickstart script, make sure it does include the `cdrom` option.
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
    --os-variant detect=off \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --name virtual-desktop \
    --boot uefi \
    --cpu host-model,topology.sockets=1,topology.cores=2,topology.threads=1 \
    --vcpus 2 \
    --memory 4096 \
    --video virtio \
    --graphics spice,listen=none \
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
    --disk path=/var/lib/libvirt/images/phyllome-desktop.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=https://download.fedoraproject.org/pub/fedora/linux/releases/35/Everything/x86_64/os/ \
    --extra-args="inst.ks=https://raw.githubusercontent.com/PhyllomeOS/phyllomeos/main/leaves/virtual-desktop.cfg"
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