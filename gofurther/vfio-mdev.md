---
title: Virtual Function I/O Mediated devices (vfio-mdev)
description: Create and Configure Virtual Function I/O Mediated devices (vfio-mdev)
published: true
date: 2023-05-14T20:10:36.548Z
tags: 
editor: markdown
dateCreated: 2022-07-21T21:10:41.046Z
---

# Configure *vfio-mdev*

> These instructions only cover **Intel GPUs** that are compatible with *vfio-mdev* (5th to 10th generation). Since generation 11th, *vfio-mdev* has been superseded by *SR-IOV*.
{.is-warning}

GPUs compatible with [Virtual Function I/O Mediated devices](https://www.kernel.org/doc/html/latest/driver-api/vfio-mediated-device.html) (vfio-mdev) can be split into multiple virtual GPUs (vGPUs). 

Then, these vGPUs can be assigned to virtual machines or containers.

Contrary to paravirtualized GPUs (e.g. *virtio-gpu*), vGPUs can use the same driver as their parent GPU (e.g. a guest compatible with an Intel GPUs will be able to leverage an Intel-based vGPUs)

## Preparation

* Make sure the GRUB has been updated after [the first boot](https://wiki.phyllo.me/getstarted/disk#update-grub-and-reboot)

## Procedure

### Create a virtual GPU

List available GPUs using the `mdevctl` software:

```
mdevctl types
```

```
0000:00:02.0
  i915-GVTg_V5_1
    Available instances: 1
    Device API: vfio-pci
    Description: low_gm_size: 512MB, high_gm_size: 2048MB, fence: 4, resolution: 1920x1200, weight: 16
  i915-GVTg_V5_2
    Available instances: 2
    Device API: vfio-pci
    Description: low_gm_size: 256MB, high_gm_size: 1024MB, fence: 4, resolution: 1920x1200, weight: 8
  i915-GVTg_V5_4
    Available instances: 5
    Device API: vfio-pci
    Description: low_gm_size: 128MB, high_gm_size: 512MB, fence: 4, resolution: 1920x1200, weight: 4
  i915-GVTg_V5_8
    Available instances: 7
    Device API: vfio-pci
    Description: low_gm_size: 64MB, high_gm_size: 384MB, fence: 4, resolution: 1024x768, weight: 2
```

> Increasing the memory allocated to the GPU in the BIOS/EFI may increase the number and kind of available instances.
{.is-info}


In this case, the `i915-GVTg_V5_4` kind seems to offer the best trade-offs between the available resolution and the number of available instances.

* Generate a universally unique identifier (UUID) with the following command:

```
uuidgen
```

```
7686131b-b229-4768-a02c-35d1dbed7c66
```

* Start a vGPU based on the kind `i915-GVTg_V5_4` using the previously generated UUID
 
```
sudo mdevctl start -u 7686131b-b229-4768-a02c-35d1dbed7c66 -p 0000:00:02.0 --type i915-GVTg_V5_4
```

* Define, or make this vGPU permanent:

```
sudo mdevctl define -u 7686131b-b229-4768-a02c-35d1dbed7c66
```

* Set the vGPU to auto-start after the host boots up:

```
sudo mdevctl modify -u 7686131b-b229-4768-a02c-35d1dbed7c66 --auto
``` 

* Finally, verify that the vGPU has successfully been created and is set to auto-start:

```
mdevctl list -d
``` 

```
7686131b-b229-4768-a02c-35d1dbed7c66 0000:00:02.0 i915-GVTg_V5_4 auto (active)
```

### Assign a vGPU to a virtual machine

* Add that segment to a virtual machine's definition. Make sure the provided `uuid` matches the previously generated UUID.

```
<domain type="kvm">
[...]
	<device>
[...]
    <hostdev mode="subsystem" type="mdev" managed="no" model="vfio-pci" display="on" ramfb="on">
      <source>
        <address uuid="7686131b-b229-4768-a02c-35d1dbed7c66"/>
      </source>
      <address type="pci" domain="0x0000" bus="0x09" slot="0x00" function="0x0"/>
    </hostdev>
[...]
	</device>
[...]
</domain>
```

> Notice that the RAMFB is set to on, which activates Drect Memory Access Buffers (DMA-BUFs), making the output of a virtual monitor available before the guest operating system takes over. 
{.is-info}

## Remove any video device or display devices

* Remove any video device such as `virtio-gpu` and set the last one to the `none`.

```
<domain type="kvm">
[...]
	<device>
[...]
    <video>
    	<model type="none"/>
    </video>
[...]
	</device>
[...]
</domain>
```

* Then starts the domain

## Configure Spice / SDL

*To-do*

## Troubleshooting

### No or low number of available instances 

Increasing the memory allocated to the GPU (a.k.a. the GPU aperture size) may increase the number of available instances.

Some computers allow you to modify the memory allocated or shared with the integrated GPU, which may allow you to create more vGPUs.

* Before the host operating system boots up, enter the BIOS/UEFI and look for a setting called *GPU aperture size*, or *GPU shared memory*. 

* Use the highest possible value.

> The memory will be reserved to the GPU, so make sure you have enough leftover memory to accomodate both the GPU and your operating system. 
{.is-info}

## Resources

* Official page for vfio-mdev: https://www.kernel.org/doc/html/latest/driver-api/vfio-mediated-device.html
* Archlinux's *must-read entry* on Intel GVT-g: https://wiki.archlinux.org/title/Intel_GVT-g
* DMA-BUF Linux documentation: https://www.kernel.org/doc/html/latest/driver-api/dma-buf.html
