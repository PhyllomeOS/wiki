---
title: Kernel modules
description: 
published: true
date: 2023-02-05T11:36:49.334Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:58:03.276Z
---

# Host-specific configuration and information

> Section under construction
{.is-warning}

## Hardware-assisted virtualization 

> Section under construction
{.is-warning}

## Nested virtualization

> Section under construction
{.is-warning}


## Linux virtualization-related kernel modules 

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
