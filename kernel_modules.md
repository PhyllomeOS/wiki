---
title: Kernel modules for virtualization
description: List of Linux kernel modules related to virtualization
published: true
date: 2021-08-12T12:50:48.233Z
tags: 
editor: markdown
dateCreated: 2021-08-12T12:50:48.233Z
---

# List

## Kernel modules on a guest-hypervisor

This list is only concerned about kernel modules that relates to virtualization. Their description is fetched using the `modinfo` command.

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