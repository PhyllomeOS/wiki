---
title: Virtual Function I/O Mediated devices (vfio-mdev)
description: Create and Configure Virtual Function I/O Mediated devices (vfio-mdev)
published: true
date: 2025-04-01T09:09:10.701Z
tags: 
editor: markdown
dateCreated: 2022-07-21T21:10:41.046Z
---

# *vfio-mdev* configuration

> These instructions only cover **Intel GPUs** that are compatible with *vfio-mdev* (5th to 10th generation). Since generation 11th, *vfio-mdev* has been superseded by *SR-IOV*.
{.is-warning}

[Virtual Function I/O Mediated devices](https://www.kernel.org/doc/html/latest/driver-api/vfio-mediated-device.html) (vfio-mdev) allows a physical GPU to be split into multiple virtual GPUs (vGPU). Such a vGPU can then be assigned to a virtual machine or a container.

Contrary to paravirtualized GPUs (e.g. *virtio-gpu*), vGPUs can use the same driver as their parent GPU (e.g. a guest compatible with an Intel GPUs will be able to leverage an Intel-based vGPUs)

## Preparation

* [Install](/deploy/install) the *Phyllome OS Desktop II*

* Make sure the GRUB has been updated after the first boot: 
`# grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg`

## Procedure

### Create a virtual GPU

List all available vGPUs types:

```
$ mdevctl types
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

> Allocating more memory to the GPU in the platform firmware may increase the number of vGPUs one can create. See [Troubleshooting](#troubleshooting) section below.
{.is-info}

In the example above, the `i915-GVTg_V5_4` virtual type seems to offer the best trade-offs between the available resolution and the number of available instances.

* Generate a universally unique identifier (UUID) with the following command:

```
$ uuidgen
```

```
$ 7686131b-b229-4768-a02c-35d1dbed7c66
```

* Start a vGPU based on the kind `i915-GVTg_V5_4` using the previously generated UUID
 
```
# mdevctl start -u 7686131b-b229-4768-a02c-35d1dbed7c66 -p 0000:00:02.0 --type i915-GVTg_V5_4
```

* Define, or make this vGPU permanent:

```
# mdevctl define -u 7686131b-b229-4768-a02c-35d1dbed7c66
```

* Set the vGPU to auto-start after the host boots up:

```
# mdevctl modify -u 7686131b-b229-4768-a02c-35d1dbed7c66 --auto
``` 

* Finally, verify that the vGPU has successfully been created and is set to auto-start:

```
$ mdevctl list -d
``` 

```
$ 7686131b-b229-4768-a02c-35d1dbed7c66 0000:00:02.0 i915-GVTg_V5_4 auto (active)
```

### Remove any video device or display devices

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

### Assign a vGPU to a virtual machine

* Add that segment to a virtual machine's definition. Make sure the provided `uuid` matches the previously generated UUID.

```
<domain type="kvm">
[...]
	<device>
[...]
    <hostdev mode="subsystem" type="mdev" managed="no" model="vfio-pci" display="off" ramfb="off">
      <source>
        <address uuid="7686131b-b229-4768-a02c-35d1dbed7c66"/>
      </source>
    </hostdev>
[...]
	</device>
[...]
</domain>
```

* Start the machine in headless mode. It is possible to connect to this machine over a console interface. 

### Add a display device

- Add a Spice display device

```
	<device>
[...]
		<graphics type="spice">
  			<listen type="none"/>
  		<gl enable="yes" rendernode="/dev/dri/by-path/pci-0000:00:02.0-render"/>
		</graphics>
[...]
	</device>
```

> When associated with OpenGL, Spice will only work locally
{.is-info}

- Modify the vGPU setting to set display and RAMFB to *on* 

```
<domain type="kvm">
[...]
	<device>
[...]
    <hostdev mode="subsystem" type="mdev" managed="no" model="vfio-pci" display="on" ramfb="on">
      <source>
        <address uuid="7686131b-b229-4768-a02c-35d1dbed7c66"/>
      </source>
    </hostdev>
[...]
	</device>
[...]
</domain>
```

> RAMFB is set to on, which activates Drect Memory Access Buffers (DMA-BUFs), making the output of a virtual monitor available before the guest operating system takes over
{.is-info}

* Then starts the domain

## Troubleshooting

### Low number of available vGPU instances 

On some computers, it is possible to increase the system memory allocated to the integrated GPU. By doing so, you may be able to create more vGPUs.

* Before the host operating system boots up, enter the BIOS/UEFI and look for a setting called *GPU aperture size* or *GPU shared memory*

* Use the highest possible value, but not higher than the available system memory

> System memory will be reserved for the GPU, so make sure you have enough system memory to accomodate both the GPU and your operating system. For instance, if you have a total of 16GB of system memory, it is recommended to allocate no more than 4GB to the GPU
{.is-info}

### Not all vGPUs are marked as active

In the example below, two vGPUs are inactive. Attempts to enable them are failing.

```
$ mdevctl list -d
5d189f35-d83b-48a8-b8d1-ac1684873493 0000:00:02.0 i915-GVTg_V5_4 auto (active)
7686131b-b229-4768-a02c-35d1dbed7c66 0000:00:02.0 i915-GVTg_V5_4 auto (active)
8aec14d3-cb64-40ff-8347-9a872180f4f2 0000:00:02.0 i915-GVTg_V5_4 auto
90f22bd6-d269-4afd-9560-ece3c6e93b0b 0000:00:02.0 i915-GVTg_V5_4 auto (active)
a4f23c92-5889-4ce9-b4a6-4d2b786a6b85 0000:00:02.0 i915-GVTg_V5_4 auto
```

In the said configuration, there is 2GB of GPU shared allocated to the physical GPU. As each of such vGPUs type requires 512MB, it cannot equate or exceed the 2GB of shared GPU memory. 

## Resources

* Official page for vfio-mdev: https://www.kernel.org/doc/html/latest/driver-api/vfio-mediated-device.html
* Arch Linux's *must-read entry* on Intel GVT-g: https://wiki.archlinux.org/title/Intel_GVT-g
* DMA-BUF Linux documentation: https://www.kernel.org/doc/html/latest/driver-api/dma-buf.html

---

*[**Go to parent page**](https://wiki.phyllo.me/)*