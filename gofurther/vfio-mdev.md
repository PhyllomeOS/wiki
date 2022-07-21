---
title: Virtual Function I/O Mediated devices (vfio-mdev)
description: Create and Configure Virtual Function I/O Mediated devices (vfio-mdev)
published: true
date: 2022-07-21T21:23:57.267Z
tags: 
editor: markdown
dateCreated: 2022-07-21T21:10:41.046Z
---

# Configure Virtual Function I/O Mediated devices (vfio-mdev)

Virtual Function I/O Mediated devices (vfio-mdev) allows you to split your GPU into virtual GPUs (vGPus), which are multiple virtual instances that can be managed using the native driver of your GPU. 

These instructions only cover Intel GPUs that are compatible with Virtual Function I/O (VFIO) Mediated devices (gen 5th to gen 9th, perhaps 10th). 

For Xe Intel graphics (11th and onward) and other cards, use SR-IOV-based GPUs.

## Preparation

* Make sure to update the grub first

```
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

* Reboot

```
Reboot
```

* Modify available GPU Aperture size (GPU memory) in the BIOS/UEFI.

```
To-do
```

## Create a virtual GPU

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

* You may need to increase GPU aperture size, or memory, if there is no available instance


The `i915-GVTg_V5_4` kind seems to offer the best trade-offs between the available resolution and the number of available instances.

* Generate unique id

```
uuidgen
```

```
7686131b-b229-4768-a02c-35d1dbed7c66
```

* Start a vGPU based off this id and of type `i915-GVTg_V5_4`
 
```
sudo mdevctl start -u 7686131b-b229-4768-a02c-35d1dbed7c66 -p 0000:00:02.0 --type i915-GVTg_V5_4
```

* Define, or make this vGPU permanent.

```
sudo mdevctl define -u 7686131b-b229-4768-a02c-35d1dbed7c66
```

* Set it to auto-start when the host has boot up.

```
sudo mdevctl modify -u 7686131b-b229-4768-a02c-35d1dbed7c66 --auto
``` 

* Verify it has successfully been created

```
mdevctl list -d
``` 

```
7686131b-b229-4768-a02c-35d1dbed7c66 0000:00:02.0 i915-GVTg_V5_4 auto (active)
```

## Assign a virtual GPU to a virtual machine

* Add that segment to a virtual machine's definition. Modify the UUID address according to the previously generated UUID.

```
    <hostdev mode="subsystem" type="mdev" managed="no" model="vfio-pci" display="on" ramfb="on">
      <source>
        <address uuid="7686131b-b229-4768-a02c-35d1dbed7c66"/>
      </source>
      <address type="pci" domain="0x0000" bus="0x09" slot="0x00" function="0x0"/>
    </hostdev>
```

* Notice RAMFB option, which allows to see the output of a virtual monitor before an operating system takes over.

## Remove any video device

* Remove any video device


## Resources

* Official page: https://www.kernel.org/doc/html/latest/driver-api/vfio-mediated-device.html
* Archlinux's entry on Intel GVT-g: https://wiki.archlinux.org/title/Intel_GVT-g
