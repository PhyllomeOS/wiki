---
title: Linux family
description: 
published: true
date: 2022-01-11T14:49:23.674Z
tags: 
editor: markdown
dateCreated: 2021-11-12T15:27:40.366Z
---

# Unattended deployment of RPM-based guests

* `virt-install` is a command-line utility that can be used to create virtual machines. It comes preinstalled with Phyllome OS. 

## Remote

* The following command will deploy a virtual machine with a stripped-down GNOME desktop environment. Adjust the settings according to your needs.

> Please verify the content of [the kickstart script](https://raw.githubusercontent.com/PhyllomeOS/phyllomeos/main/dishes/virtual-desktop.cfg) used to automate the installation. You may replace the kickstart script by a kickstart script of your choice.
{.is-info}

```
virt-install \
    --connect qemu:///system \
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
    --disk path=/var/lib/libvirt/images/virtual-desktop.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=https://download.fedoraproject.org/pub/fedora/linux/releases/35/Everything/x86_64/os/ \
    --extra-args="https://raw.githubusercontent.com/PhyllomeOS/phyllomeos/main/dishes/virtual-desktop.cfg"
```

## Automated installation using a local kickstart file 

* Use the following `wget` command to fetch a standalone kickstart file made to deploy a stripped-down desktop system with GNOME Shell, and put it in the working directory

```
wget https://raw.githubusercontent.com/PhyllomeOS/phyllomeos/main/dishes/virtual-desktop.cfg
```

> Please verify the content of the script if you intent to use this virtual machine in production, for instance by using the following command `cat virtual-desktop.cfg`
{.is-info}

> If using a custom kickstart script, make sure it includes the `repo` information
{.is-warning}

* Deploy a stripped down desktop based on GNOME Shell using the local kickstart file previously downloaded

```
virt-install \
    --connect qemu:///system \
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
    --disk path=/var/lib/libvirt/images/virtual-desktop.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=https://download.fedoraproject.org/pub/fedora/linux/releases/35/Everything/x86_64/os/ \
    --initrd-inject virtual-desktop.cfg --extra-args "inst.ks=file:/virtual-desktop.cfg"
```

### Local deployment without installation

* The idea here is to define a virtual machine and use the `netboot.xyz.iso` as a way to boot into an installer. 

```
virt-install \
    --connect qemu:///system \
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
    --disk none \
    --cdrom=/var/lib/libvirt/iso/netboot.xyz.iso \
    --install no_install=yes
```


## Automated installation using an ISO file and a local kickstart file

> **Warning**: doesn't work as intended. The kickstart file won't have to be modified to include the `cdrom` option and the ISO would have to include the necessary packages. 
{.is-danger}


* Use the following `wget` command to fetch the official Fedora Server ISO file and to put it in the current working directory

```
wget https://download.fedoraproject.org/pub/fedora/linux/releases/35/Server/x86_64/iso/Fedora-Server-dvd-x86_64-35-1.2.iso
```
> Please [verify your download](https://getfedora.org/en/security/) if you intent to use this virtual machine in production
{.is-info}

Move the file to `/var/lib/libvirt/iso`:
```
mv Fedora-Server-dvd-x86_64-35-1.2.iso /var/lib/libvirt/iso
``` 
* Use the following `wget` command to fetch a standalone kickstart file made to deploy a stripped down desktop based on GNOME Shell, and put it in the working directory

```
wget https://raw.githubusercontent.com/PhyllomeOS/phyllomeos/main/dishes/virtual-desktop.cfg
```

> Please verify the content of the script if you intent to use this virtual machine in production, for instance by using the following command `cat virtual-desktop.cfg`
{.is-info}

> If you use a custom kickstart script, make sure it does include the `cdrom` option.
{.is-warning}

* Deploy a UEFI-based machine with Fedora Server using the relative path of the local kickstart file

```
virt-install \
    --connect qemu:///system \
    --os-variant detect=off \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --name virtual-desktop-cdrom \
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
    --disk path=~/.local/share/libvirt/images/virtual-phyllome-desktop-cdrom.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=/tmp/Fedora-Everything-netinst-x86_64-35-1.2.iso \
    --initrd-inject virtual-desktop-cdrom.cfg --extra-args "inst.ks=file:/virtual-phyllome-desktop-cdrom.cfg"
```

---
