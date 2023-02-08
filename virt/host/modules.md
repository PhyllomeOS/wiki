---
title: Kernel modules
description: 
published: true
date: 2023-02-08T18:42:56.268Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:58:03.276Z
---

# Host configuration and information

> Section under construction
{.is-warning}

## IOMMU-enablement

By default, Linux distributions do not generally enable IOMMU groups, a prerequisite to share real hardware to virtual machines using modern virtualization techniques.

### With GRUB as a bootloader

* For Intel CPUs, the following command adds the necessary bits:

```
# sed -i 's/\(quiet\)/\1 intel_iommu=on iommu=pt rd.driver.pre=vfio-pci/i' /etc/default/grub # Load kernel modules in GRUB.
``` 

> `iommu=pt` makes sure that only devices that can be pass to a virtual machine will be flagged as such. `rd.driver.pre=vfio-pci` makes sure that the `vfio-pci` driver is loaded early in the boot process.
{.is-info}

* For AMD CPUs, IOMMU groups are created by default, so the command is a bit different:

```
# sed -i 's/\(quiet\)/\1 iommu=pt rd.driver.pre=vfio-pci/i' /etc/default/grub # Load kernel modules in GRUB.
``` 

* It should then look like this:

```
$ cat /etc/default/grub
```

Then, one needs to regenerate GRUB.

* On Debian-based distributions:
```
# update-grub
```

### With systemd-boot as a bootloader

> Section under construction
{.is-warning}

## Nested virtualization

Nested virtualization is rarely enabled on Linux distributions. 

* For Intel-based CPUs:

``` 
echo "options kvm_intel nested=1" >> /etc/modprobe.d/kvm.conf
```

* For AMD-based CPUs:

``` 
echo "options kvm_amd nested=1" >> /etc/modprobe.d/kvm.conf
```

### VMCS Shadowing (Intel-only)

* Enabling VMCS shadowing may give [a performance boost](https://storpool.com/blog/nested-virtualization-with-kvm-and-opennebula) on Haswell CPUs and later. Append that `enable_shadow_vmcs=1` to *kvm.conf*. It should look like that:

```
cat /etc/modprobe.d/kvm.conf
options kvm_intel nested=1 enable_shadow_vmcs=1
```

## Virtualization-related kernel modules 

This list is only concerned about kernel modules that relates to virtualization. Their description can be found using the `modinfo` command.

```
kvm_intel # "" 
kvm_amd # ""
kvm # Kernel virtual machine module for Linux
```

```
vfio_pci # "VFIO PCI - User Level meta-driver"
vfio_virqfd # "IRQFD support for VFIO bus drivers"
vfio_iommu_type1 # "Type1 IOMMU driver for VFIO"
vfio # "VFIO - User Level meta-driver"
vfio_mdev # "VFIO based driver for Mediated device"    
```

```
mdev # "Mediated device Core Driver"
```

```
vhost_net # "Host kernel accelerator for virtio net"
vhost # "Host kernel accelerator for virtio"
vhost_iotlb # "VHOST IOTLB"
```

```
tap # ""
tun # "Universal TUN/TAP device driver"
```

```
virtio_net # "Virtio network driver"
virtio_balloon # "Virtio balloon driver"
virtio_blk # "Virtio block driver"
virtio_console # "Virtio console driver"
virtio_scsi # "Virtio SCSI HBA driver"
virtio_gpu # "Virtio GPU driver"
virtio_dma_buf #
```

```
qemu_fw_cfg # "QEMU fw_cfg sysfs support"
irqbypass # "IRQ bypass manager utility module"
net_failover # "Failover driver for Paravirtual drivers"
failover # "Generic failover infrastructure/interface"
```

## Ressources

* https://storpool.com/blog/nested-virtualization-with-kvm-and-opennebula/