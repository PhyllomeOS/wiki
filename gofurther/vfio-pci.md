---
title: Virtual Function I/O passthrough (vfio-pci)
description: Pass a physical device to a guest sysstem
published: true
date: 2025-04-01T11:26:11.765Z
tags: 
editor: markdown
dateCreated: 2025-04-01T11:18:43.924Z
---

# *vfio-pci* configuration

[Virtual Function I/O](https://www.kernel.org/doc/html/latest/driver-api/vfio.html) (vfio-pci) passthrough allows for a single physical device to be assigned to a virtual machine or container.


## Preparation

* [Install](/deploy/install) any version of *Phyllome OS*

* Make sure the GRUB has been updated after the first boot: 
`# grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg`

## Isolate the physical device

* Copy paste the following:

```
$ shopt -s nullglob
for g in $(find /sys/kernel/iommu_groups/* -maxdepth 0 -type d | sort -V); do
    echo "IOMMU Group ${g##*/}:"
    for d in $g/devices/*; do
        echo -e "\t$(lspci -nns ${d##*/})"
    done;
done;
```

``` 
IOMMU Group 0:
	00:02.0 VGA compatible controller [0300]: Intel Corporation Iris Pro Graphics 580 [8086:193b] (rev 09)
IOMMU Group 1:
	00:00.0 Host bridge [0600]: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Host Bridge/DRAM Registers [8086:1910] (rev 0a)
IOMMU Group 2:
	00:08.0 System peripheral [0880]: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model [8086:1911]
IOMMU Group 3:
	00:14.0 USB controller [0c03]: Intel Corporation 100 Series/C230 Series Chipset Family USB 3.0 xHCI Controller [8086:a12f] (rev 31)
	00:14.2 Signal processing controller [1180]: Intel Corporation 100 Series/C230 Series Chipset Family Thermal Subsystem [8086:a131] (rev 31)
IOMMU Group 4:
	00:16.0 Communication controller [0780]: Intel Corporation 100 Series/C230 Series Chipset Family MEI Controller #1 [8086:a13a] (rev 31)
IOMMU Group 5:
	00:1c.0 PCI bridge [0604]: Intel Corporation 100 Series/C230 Series Chipset Family PCI Express Root Port #1 [8086:a110] (rev f1)
IOMMU Group 6:
	00:1c.1 PCI bridge [0604]: Intel Corporation 100 Series/C230 Series Chipset Family PCI Express Root Port #2 [8086:a111] (rev f1)
IOMMU Group 7:
	00:1c.2 PCI bridge [0604]: Intel Corporation 100 Series/C230 Series Chipset Family PCI Express Root Port #3 [8086:a112] (rev f1)
IOMMU Group 8:
	00:1c.4 PCI bridge [0604]: Intel Corporation 100 Series/C230 Series Chipset Family PCI Express Root Port #5 [8086:a114] (rev f1)
IOMMU Group 9:
	00:1d.0 PCI bridge [0604]: Intel Corporation 100 Series/C230 Series Chipset Family PCI Express Root Port #9 [8086:a118] (rev f1)
IOMMU Group 10:
	00:1d.4 PCI bridge [0604]: Intel Corporation 100 Series/C230 Series Chipset Family PCI Express Root Port #13 [8086:a11c] (rev f1)
IOMMU Group 11:
	00:1f.0 ISA bridge [0601]: Intel Corporation HM170 Chipset LPC/eSPI Controller [8086:a14e] (rev 31)
	00:1f.2 Memory controller [0580]: Intel Corporation 100 Series/C230 Series Chipset Family Power Management Controller [8086:a121] (rev 31)
	00:1f.3 Audio device [0403]: Intel Corporation 100 Series/C230 Series Chipset Family HD Audio Controller [8086:a170] (rev 31)
	00:1f.4 SMBus [0c05]: Intel Corporation 100 Series/C230 Series Chipset Family SMBus [8086:a123] (rev 31)
IOMMU Group 12:
	00:1f.6 Ethernet controller [0200]: Intel Corporation Ethernet Connection (2) I219-LM [8086:15b7] (rev 31)
IOMMU Group 13:
	02:00.0 SD Host controller [0805]: O2 Micro, Inc. SD/MMC Card Reader Controller [1217:8621] (rev 01)
IOMMU Group 14:
	03:00.0 Network controller [0280]: Intel Corporation Wireless 8260 [8086:24f3] (rev 3a)
IOMMU Group 15:
	3d:00.0 Non-Volatile memory controller [0108]: Samsung Electronics Co Ltd NVMe SSD Controller SM951/PM951 [144d:a802] (rev 01)
IOMMU Group 16:
	3e:00.0 Non-Volatile memory controller [0108]: Intel Corporation SSD 660P Series [8086:f1a8] (rev 03)
IOMMU Group 17:
lspci: -s: Invalid slot number
	
IOMMU Group 18:
lspci: -s: Invalid slot number
	
IOMMU Group 19:
lspci: -s: Invalid slot number



```
List all available vGPUs types:

```
$ mdevctl types
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

> Allocating more memory to the GPU in the platform firmware may increase the number of vGPUs one can create. See [*Troubleshooting*](#troubleshooting) section below
{.is-info}

In the example above, the `i915-GVTg_V5_4` virtual type seems to offer the best trade-offs between the available resolution and the number of available instances.

* Generate a universally unique identifier (UUID) with the following command:

```
$ uuidgen
7686131b-b229-4768-a02c-35d1dbed7c66
```

* Start a vGPU based on the kind `i915-GVTg_V5_4` using the previously generated UUID
 
```
# mdevctl start --uuid 7686131b-b229-4768-a02c-35d1dbed7c66 -p 0000:00:02.0 --type i915-GVTg_V5_4
```

* Define, or make this vGPU permanent:

```
# mdevctl define --uuid 7686131b-b229-4768-a02c-35d1dbed7c66
```

* Set the vGPU to auto-start after the host boots up:

```
# mdevctl modify --uuid 7686131b-b229-4768-a02c-35d1dbed7c66 --auto
``` 

* Finally, verify that the vGPU has successfully been created and is set to auto-start:

```
$ mdevctl list --defined
7686131b-b229-4768-a02c-35d1dbed7c66 0000:00:02.0 i915-GVTg_V5_4 auto (active)
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

## Add a display device


## Troubleshooting

### Low number of available vGPU instances 



### Not all vGPUs are marked as active


## Resources

* Official page for vfio-mdev: https://www.kernel.org/doc/html/latest/driver-api/vfio-mediated-device.html
* Arch Linux's *must-read entry* on Intel GVT-g: https://wiki.archlinux.org/title/Intel_GVT-g
* DMA-BUF Linux documentation: https://www.kernel.org/doc/html/latest/driver-api/dma-buf.html

---

*[**Go to parent page**](https://wiki.phyllo.me/)*