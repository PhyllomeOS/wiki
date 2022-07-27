---
title: Virtual Function I/O Mediated devices (vfio-mdev)
description: Create and Configure Virtual Function I/O Mediated devices (vfio-mdev)
published: true
date: 2022-07-27T23:53:40.933Z
tags: 
editor: markdown
dateCreated: 2022-07-21T21:10:41.046Z
---

# Configure Virtual Function I/O Mediated devices

Virtual Function I/O Mediated devices (vfio-mdev) allows you to split a compatible GPU into multiple virtual GPUs (vGPUs). These vGPUs can then be assigned to a virtual machine, just as real GPUs.

> These instructions only cover Intel GPUs that are compatible with vfio-mdev (5th to 10th generation). Since generation 11th, Intel graphics do not support vfio-mdev but SR-IOV.
{.is-info}

## Preparation

### Update the GRUB 

* On a freshly deployed edition of Phyllome OS optimized for Intel Graphics such as [Phyllome OS Desktop II](https://wiki.phyllo.me/deploy/rightforyou), make sure that the GRUB has been updated.

```
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

* Then reboot your computer

```
sudo reboot
```

### Modify GPU Memory in BIOS/UEFI

> Only available for Intel Graphics cards
{.is-info}

Some computers allow you to modify the GPU memory allocated your desktop-based computers. It will reserve system memory for the GPUs.

To do so, you need to enter the BIOS/UEFI and to look for a setting called GPU Aperture size, or GPU memory. 

Use the highest value possible, but make sure you have enough system memory to accomodate both the GPU and your operating system. 

## Create a virtual GPU

Upon reboot, you should then be able to list available GPUs using the `mdevctl` command. 

* List available virtual GPUs

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

* You may need to increase GPU aperture size if there is no available instance.

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

* Define, or make this vGPU permanent.

```
sudo mdevctl define -u 7686131b-b229-4768-a02c-35d1dbed7c66
```

* Set the vGPU to auto-start after the host boots up, so that it is available to guest virtual machines without further action 

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

Great you have 

## Assign a virtual GPU to a virtual machine

* Add that segment to a virtual machine's definition. Make sure the provided ```uuid``` matches the previously generated UUID.

```
<domain>
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

> Notice that the RAMFB is set to on, which activates Drect Memory Access Buffers (DMA-BUFs), making available the output of a virtual monitor before the guest operating system takes over 
{.is-info}

## Configure Spice / SDL

*To-do*

## Remove any video device

* Remove any video device such as `virtio-gpu` and set the last one to the `none`.


```
<domain>
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

## Resources

* Official page for vfio-mdev: https://www.kernel.org/doc/html/latest/driver-api/vfio-mediated-device.html
* Archlinux's entry on Intel GVT-g: https://wiki.archlinux.org/title/Intel_GVT-g
* DMA-BUF Linux documentation: https://www.kernel.org/doc/html/latest/driver-api/dma-buf.html
