---
title: Linux family
description: 
published: true
date: 2025-03-31T14:27:25.512Z
tags: 
editor: markdown
dateCreated: 2021-11-12T15:27:40.366Z
---

# Unattended deployment of an RPM-based guest

* `virt-install` is a command-line utility that can be used to create virtual machines. It comes preinstalled with Phyllome OS. 

## Deployment using a hosted kickstart file

* The following command will create a virtual machine with a 10G virtual disk and deploy an RPM-based operating system with a stripped-down GNOME desktop environment inside. Most settings can be modified after the installation.

> Please verify the content of [the kickstart script](https://raw.githubusercontent.com/PhyllomeOS/phyllomeos/main/dishes/virtual-desktop.cfg) used to automate the installation. You may replace the kickstart script by a kickstart script of your choice.
{.is-info}

* Copy the command below, open you favorite terminal, paste the content, and press <kbd>enter</kbd>.  

```
virt-install \
    --connect qemu:///system \
    --os-variant fedora41 \
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
    --network type=default,model=virtio \
    --controller type=virtio-serial \
    --controller type=usb,model=none \
    --controller type=scsi,model=virtio-scsi \
    --input type=keyboard,bus=virtio \
    --input type=tablet,bus=virtio \
    --rng /dev/urandom,model=virtio \
    --disk path=/var/lib/libvirt/images/virtual-desktop.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=https://download.fedoraproject.org/pub/fedora/linux/releases/41/Everything/x86_64/os/ \
    --extra-args="inst.ks=https://raw.githubusercontent.com/PhyllomeOS/phyllomeos/main/dishes/virtual-desktop.cfg"
```

## Deployment using a local kickstart file

* Use the following `wget` command to fetch a standalone kickstart file made to deploy a stripped-down desktop system with GNOME Shell, and put it in the working directory

```
wget https://raw.githubusercontent.com/PhyllomeOS/phyllomeos/main/dishes/virtual-desktop.cfg
```

> Please verify the content of the script if you intent to use this virtual machine in production, for instance by using the following command `cat virtual-desktop.cfg`
{.is-info}

* Deploy a stripped-down desktop based on GNOME Shell using the local kickstart file previously downloaded

```
virt-install \
    --connect qemu:///system \
    --os-variant fedora41 \
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
    --network type=default,model=virtio \
    --controller type=virtio-serial \
    --controller type=usb,model=none \
    --controller type=scsi,model=virtio-scsi \
    --input type=keyboard,bus=virtio \
    --input type=tablet,bus=virtio \
    --rng /dev/urandom,model=virtio \
    --disk path=/var/lib/libvirt/images/virtual-desktop.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=https://download.fedoraproject.org/pub/fedora/linux/releases/40/Everything/x86_64/os/ \
    --initrd-inject virtual-desktop.cfg --extra-args "inst.ks=file:/virtual-desktop.cfg"
```

---

*[**Go to parent page**](https://wiki.phyllo.me/)*