---
title: Automatic deployment of a Fedora guest automatically 
description: Deploy a Fedora automatically with virt-install
published: true
date: 2021-08-12T10:06:58.917Z
tags: 
editor: markdown
dateCreated: 2021-08-12T10:06:58.917Z
---

# Virt-install

## Introduction

*virt-install* is a command-line utility to install virtual machines.

### Installation

*virt-install* tool is part of the _______ package in Fedora :

```
# dnf install ________
```

## The simpliest command

Use the following command to automatically launch the fedora installation process. It will also automatically create a disk image to install Fedora on. 

```
virt-install --install fedora32
```
* Note : the virt-install package that comes with Fedora 34 doesn't work yet with argument *fedora34*

## Going further

### Don't launch any installation, just create a VM

```
virt-install \
    --connect qemu:///system \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --boot uefi \
    --vcpus 2 \
    --cpu host-model,topology.sockets=1,topology.cores=1,topology.threads=2 \
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
    --disk none \
    --install no_install=yes  
```

### Launch the installation for Fedora 34 server

* KVM-accelerated EFI-based machine, using the Q35 chipset, with a virtio-based graphic and network card. Connection through spice. A 10G disk image is created under the default location libvirt location. 

```
    --location /var/lib/libvirt/iso/Fedora-Server-dvd-x86_64-34-1.2.iso \
    --install no_install=no      
```
### Automated installation with local iso and kickstart

Note : requires an Internet connection

* Remove the following 
```
    --disk none \
    --install no_install=yes  
```

* Replace it with : 
```
    --disk path=/var/lib/libvirt/images/vmd.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=/var/lib/libvirt/iso/Fedora-Server-dvd-x86_64-34-1.2.iso \
    --extra-args="inst.ks=https://git.phyllo.me/home/kickstart/raw/branch/master/leaves/vmd.cfg"
```

### vmd, 'v' for virtual machine, 'm' for minimal, 'd' for development only.

```
virt-install \
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
    --disk path=/var/lib/libvirt/images/vmd.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=/var/lib/libvirt/iso/Fedora-Server-dvd-x86_64-34-1.2.iso \
    --extra-args="inst.ks=https://git.phyllo.me/home/kickstart/raw/branch/master/leaves/vmd.cfg"
```

* Alternatively, the following location can be picked [Doesn't work as of now. Would need to modify the kickstart, perhaps]

```
virt-install \
    --connect qemu:///system \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --name vmd-internet \
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
    --disk path=/var/lib/libvirt/images/vmd-internet.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=https://download.fedoraproject.org/pub/fedora/linux/releases/34/Server/x86_64/os \
    --extra-args="inst.ks=https://git.phyllo.me/home/kickstart/raw/branch/master/leaves/vmd.cfg"
```

### vdmd, 'v' for virtual machine, 'd' for desktop, 'm' for minimal, 'd' for development only.

```
virt-install \
    --connect qemu:///system \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --name vdmd \
    --boot uefi \
    --cpu host-model,topology.sockets=1,topology.cores=1,topology.threads=2 \
    --vcpus 2 \
    --memory 4096 \
    --video virtio \
    --channel spicevmc \
    --autoconsole graphical \
    --sound none \
    --controller type=virtio-serial \
    --controller type=usb,model=none \
    --controller type=scsi,model=virtio-scsi \
    --network network=default,model=virtio \
    --input type=keyboard,bus=virtio \
    --input type=tablet,bus=virtio \
    --rng /dev/urandom,model=virtio \
    --disk path=/var/lib/libvirt/images/vdmd.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=/var/lib/libvirt/iso/Fedora-Server-dvd-x86_64-34-1.2.iso \
    --extra-args="inst.ks=https://git.phyllo.me/home/kickstart/raw/branch/master/leaves/vdmd.cfg"
```

### vhmd, 'v' for virtual machine, 'h' for hypervisor', 'd' for desktop, 'm' for minimal, 'd' for development only.

```
virt-install \
    --connect qemu:///system \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --name vhmd \
    --boot uefi \
    --cpu host-passthrough,topology.sockets=1,topology.cores=2,topology.threads=2 \
    --vcpus 4 \
    --memory 8192 \
    --video virtio \
    --channel spicevmc \
    --autoconsole none \
    --sound none \
    --controller type=virtio-serial,driver.iommu=on \
    --controller type=usb,model=none \
    --controller type=scsi,model=virtio-scsi,driver.iommu=on \
    --network network=default,model=virtio,driver.iommu=on \
    --input type=keyboard,bus=virtio,driver.iommu=on \
    --input type=tablet,bus=virtio,driver.iommu=on \
    --rng /dev/urandom,model=virtio,driver.iommu=on \
    --disk path=/var/lib/libvirt/images/vhmd.img,format=raw,bus=virtio,cache=writeback,size=20 \
    --location=/var/lib/libvirt/iso/Fedora-Server-dvd-x86_64-34-1.2.iso \
    --extra-args="inst.ks=https://git.phyllo.me/home/kickstart/raw/branch/master/leaves/vhmd.cfg"
```

### vhamd, 'v' for virtual machine, 'h' for hypervisor', 'a' for amd, 'm' for minimal, 'd' for development only.

```
virt-install \
    --connect qemu:///system \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --name vhadmd \
    --boot uefi \
    --cpu host-passthrough,topology.sockets=1,topology.cores=2,topology.threads=2 \
    --vcpus 4 \
    --memory 8192 \
    --video virtio \
    --channel spicevmc \
    --autoconsole none \
    --sound none \
    --controller type=virtio-serial,driver.iommu=on \
    --controller type=usb,model=none \
    --controller type=scsi,model=virtio-scsi,driver.iommu=on \
    --network network=default,model=virtio,driver.iommu=on \
    --input type=keyboard,bus=virtio,driver.iommu=on \
    --input type=tablet,bus=virtio,driver.iommu=on \
    --rng /dev/urandom,model=virtio,driver.iommu=on \
    --disk path=/var/lib/libvirt/images/vhadmd.img,format=raw,bus=virtio,cache=writeback,size=20 \
    --location=/var/lib/libvirt/iso/Fedora-Server-dvd-x86_64-34-1.2.iso \
    --extra-args="inst.ks=https://git.phyllo.me/home/kickstart/raw/branch/master/leaves/vhadmd.cfg"
```

### vhidmd, 'v' for virtual machine, 'h' for hypervisor', 'i' for intel, 'm' for minimal, 'd' for development only.

```
virt-install \
    --connect qemu:///system \
    --virt-type kvm \
    --arch x86_64 \
    --machine q35 \
    --iommu intel \
    --name vhidmd \
    --boot uefi \
    --cpu host-passthrough,topology.sockets=1,topology.cores=2,topology.threads=2 \
    --vcpus 4 \
    --memory 8192 \
    --video virtio \
    --channel spicevmc \
    --autoconsole none \
    --sound none \
    --controller type=virtio-serial,driver.iommu=on \
    --controller type=usb,model=none \
    --controller type=scsi,model=virtio-scsi,driver.iommu=on \
    --network network=default,model=virtio,driver.iommu=on \
    --input type=keyboard,bus=virtio,driver.iommu=on \
    --input type=tablet,bus=virtio,driver.iommu=on \
    --rng /dev/urandom,model=virtio,driver.iommu=on \
    --disk path=/var/lib/libvirt/images/vhidmd.img,format=raw,bus=virtio,cache=writeback,size=20 \
    --location=/var/lib/libvirt/iso/Fedora-Server-dvd-x86_64-34-1.2.iso \
    --extra-args="inst.ks=https://git.phyllo.me/home/kickstart/raw/branch/master/leaves/vhidmd.cfg"
```

### vmd, 'v' for virtual machine, 'm' for minimal, 'd' for development only. Trying with local kickstart

```
virt-install \
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
    --disk path=/var/lib/libvirt/images/vmd.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=/var/lib/libvirt/iso/Fedora-Server-dvd-x86_64-34-1.2.iso \
    --initrd-inject=/home/lukas/Projects/kickstart/vmd.cfg \
    --extra-args "ks=file:/vmd.cfg console=ttyS0"









## Doesn't work (tm)

### Automated installation with remote image 

* **to-do**
$ qemu-img create -f raw /var/lib/libvirt/images/ks.img 10G 


```
virt-install \
    --connect qemu:///system \
    --accelerate \
    --name ks2 \
    --arch x86_64 \
    --machine q35 \
    --boot uefi \
    --os-type linux \
    --os-variant fedora32 \
    --vcpus 2 \
    --memory 4096 \
    --video virtio \
    --channel spicevmc \
    --disk path=/var/lib/libvirt/images/ks2.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=https://download.fedoraproject.org/pub/fedora/linux/releases/32/Server/x86_64/os \
    --initrd-inject /var/lib/libvirt/images/ks.cfg \
    --extra-args="inst.ks=file:/var/lib/libvirt/images/ks.cfg"
```

### Automated installation with local kickstart file and local iso (works, don't touch!)

* **to-do**

```
virt-install \
    --connect qemu:///system \
    --accelerate \
    --name ks3 \
    --arch x86_64 \
    --machine q35 \
    --boot uefi \
    --os-type linux \
    --os-variant generic \
    --vcpus 2 \
    --memory 4096 \
    --video virtio \
    --channel spicevmc \
    --network network=default,model=virtio \
    --disk path=/var/lib/libvirt/images/ks3.img,format=raw,bus=virtio,cache=writeback,size=10 \
    --location=/var/lib/libvirt/iso/Fedora-Server-dvd-x86_64-34-1.2.iso \
    --extra-args="inst.ks=https://url.phyllo.me/vemsd"
```

Example with iommu
```
# virt-install \
    --name foo \
    --memory 4096 \
    --boot uefi \
    --machine q35 \
    --memtune hard_limit=4563402 \
    --disk size=15,target.bus=scsi \
    --import \
    --controller type=scsi,model=virtio-scsi,driver.iommu=on \
    --controller type=virtio-serial,driver.iommu=on \
    --network network=default,model=virtio,driver.iommu=on \
    --rng /dev/random,driver.iommu=on \
    --memballoon driver.iommu=on \
    --launchSecurity sev
```

## Description of some sub-commands

### location

--location {VALUE}
--location test.iso \
--location test.iso.iso,kernel=kernel/fookernel,initrd=kernel/fooinitrd 

Some locations :

* http://mirror.centos.org/centos-7/7/os/x86_64/
* https://download.fedoraproject.org/pub/fedora/linux/releases/34/Server/x86_64/os
* https://download.fedoraproject.org/pub/fedora/linux/releases/34/Server/x86_64/os

### misc

--import
--qemu-commandline="-display gtk,gl=on"
--description "Test VM with linux " \

### boot

--boot loader=/usr/share/OVMF/OVMF_CODE.fd,loader_ro=yes,loader_type=pflash \
--boot loader=/usr/share/OVMF/OVMF_CODE.secboot.fd,loader_ro=yes,loader_type=pflash \
--boot loader=/.../OVMF_CODE.fd,loader.readonly=yes,loader.type=pflash,nvram.template=/.../OVMF_VARS.fd,loader_secure=no
--boot loader=/usr/share/OVMF/OVMF_CODE.fd,loader.readonly=yes,loader.type=pflash,nvram.template=/usr/share/OVMF/OVMF_VARS.fd,loader_secure=no \


### virtualization

--hvm \
--paravirt \
--iommu \

### video

--video virtio \ 

### graphics

--graphics none \
--graphics spice \
--graphics type=vnc \
--graphics type=spice gl.enable gl.rendernode \ # won't work on Nvidia cards

### channel

--channel spicevmc \

### network 

--network network=default \
--network network=default,model=virtio,driver.iommu=on \
--network bridge:virbr0  \
--network network=provision,model=virtio,mac=00:11:22:33:44:00 \ 
--network network=public,model=virtio,mac=00:11:22:33:45:00 \

## controllers

--controller type=scsi,model=virtio-scsi,driver.iommu=on \
--controller type=virtio-serial,driver.iommu=on \
--controller type=usb,model=none \
--controller type=usb,model=qemu-xhci,driver.iommu=on \


### os

--os-type=Linux \
--os-variant=fedora32 \
--initrd-inject= \

### disk path

--disk path=/home/f34v.qcow2,bus=virtio,size=30 \
--disk path=/home/f34v.qcow2,format=raw,bus=virtio,cache=writeback \
--disk path=/home/f34v.qcow2,format=qcow2,cache=writeback \

### rng

--rng /dev/random,driver.iommu=on \

### console

--console pty,target_type=serial \

### memory

--memballoon driver.iommu=on \

### To be sorted

--initrd-inject=/var/lib/libvirt/images/ks.cfg \

--extra-args "ks=/var/lib/libvirt/images/ks.cfg console=ttyS0,115200n8 serial" 
--extra-args "ks=https://git.phyllo.me/home/kickstart/src/branch/master/leafs/vemsd.cfg console=ttyS0,115200n8 serial"
--extra-args "ks=file:/var/lib/libvirt/images/ks.cfg console=ttyS0"
--extra-args "ks=/var/lib/libvirt/images/ks.cfg console=ttyS0,115200n8 serial" \ 
--extra-args "inst.ks=file:/var/lib/libvirt/images/ks.cfg console=ttyS0 net.ifnames=0 biosdevname=0"

-x "ks=https://git.phyllo.me/home/kickstart/raw/branch/master/f34/ks.cfg ksdevice=eth0 ip=10.10.21.76 netmask=255.255.255.240 dns=10.10.21.1 gateway=10.10.21.100"
-x "ks=https://git.phyllo.me/home/kickstart/raw/branch/master/f34/ks.cfg ksdevice=eth0 ip=10.10.21.76 netmask=255.255.255.240 dns=10.10.21.1 gateway=10.10.21.100

## ARM

Start serial QEMU ARM VM, which requires specifying a manual kernel.
```
virt-install \
  --name armtest \
  --memory 1024 \
  --arch armv7l --machine vexpress-a9 \
  --disk /home/user/VMs/myarmdisk.img \
  --boot kernel=/tmp/my-arm-kernel,initrd=/tmp/my-arm-initrd,dtb=/tmp/my-arm-dtb,kernel_args="console=ttyAMA0 rw root=/dev/mmcblk0p3" \
  --graphics none
```
### Other commands

Uses libosinfo's unattended install support, which will perform the fedora29 install automatically without any user intervention:

`virt-install --install fedora29 --unattended`

### Virt-install with cloud-init

`virt-install --install fedora34,cloud=yes --cloud-init root-password-generate=on ssh-key=/home/user/.ssh/test_rsa.pub disable=on`

## Noticeable supported OSs

#### Android-x86 9.0                                    
`android-x86-9.0`
* http://android-x86.org/android-x86/9.0

#### CentOS 8                                             
`centos8`
* http://centos.org/centos/8

#### Clear Linux OS                                    
`clearlinux`
* http://clearlinux.org/clearlinux/rollin

#### Debian 9                                           
`debian9`
* http://debian.org/debian/9

#### Fedora 32                                           
`fedora32`
* http://fedoraproject.org/fedora/32

#### MacOS X Lion 
`macosx10.7`
* http://apple.com/macosx/10.7

#### NixOS 20.03                                        
`nixos-20.03`
* http://nixos.org/nixos/20.03

#### Ubuntu 20.04                                       
`ubuntu20.04`
* http://ubuntu.com/ubuntu/20.04

#### Microsoft Windows XP, 5.1
`winxp`
* http://microsoft.com/win/xp

#### Microsoft Windows 10 
`win10`
* http://microsoft.com/win/10

## Misc

``` 
virt-install \
    --connect=qemu:///system \
    --name="${HOSTNAME}" \
    --bridge="${BRIDGE}" \
    --mac="${MAC}" \
    --disk="${VM_IMAGE_DIR}/images/${HOSTNAME}.img,bus=virtio,size=${STORAGE}" \
    --ram="${RAM}" \
    --vcpus="${VCPUS}" \
    --autostart \
    --hvm \
    --arch x86_64 \
    --accelerate \
    --check-cpu \
    --os-type=linux \
    --force \
    --watchdog=default \
    --extra-args="ks=file:/${KS_FILE} console=tty0 console=ttyS0,115200n8 serial" \
    --initrd-inject="${KS_FQN}" \
    --graphics=none \
    --noautoconsole \
    --debug \
    --location="${ISO_FQN}"
```

## Reference 

* Great ressource : https://www.tomas.io/articles/try-fedora
* Kickstart and virt-install : https://stackoverflow.com/questions/60440478/how-to-virt-install-kvm-centos-8-using-kickstart-cfg
* http://blog.leifmadsen.com/blog/2016/12/16/creating-virtual-machines-in-libvirt-with-virt-install/
* https://fedoraproject.org/wiki/QA:Testcase_Kickstart_File_Path_Ks_Cfg
* https://www.reddit.com/r/Fedora/comments/j6cr9n/pxekickstart_fedora/
* https://bgstack15.wordpress.com/2019/07/25/use-virt-install-to-fully-automate-the-install-for-centos-fedora-with-kickstart/
* https://libvirt-users.redhat.narkive.com/gsET3DuB/virt-install-kickstart-local-file
* https://earlruby.org/2018/12/use-iso-and-kickstart-files-to-automatically-create-vms/
* https://stackoverflow.com/questions/60440478/how-to-virt-install-kvm-centos-8-using-kickstart-cfg
* https://gist.github.com/paveq/5684255
* https://stackoverflow.com/questions/60440478/how-to-virt-install-kvm-centos-8-using-kickstart-cfg
* Cloud-init reference : https://blog.wikichoon.com/2020/09/virt-install-cloud-init.html
