---
title: Virtual Function I/O passthrough (vfio-pci)
description: Pass a physical device to a guest sysstem
published: true
date: 2025-04-01T17:59:22.972Z
tags: 
editor: markdown
dateCreated: 2025-04-01T11:18:43.924Z
---

# *Vfio-pci* configuration

[Virtual Function I/O](https://www.kernel.org/doc/html/latest/driver-api/vfio.html) (vfio-pci) passthrough allows for a single physical device to be assigned to a virtual machine or container.


## Preparation

* [Install](/deploy/install) any version of *Phyllome OS*

* Make sure the GRUB has been updated after the first boot: 
`# grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg`

## Isolate the physical device

* List IOMMU groups and their associated devices (script courtesy of the [Arch Linux wiki](https://wiki.archlinux.org/title/PCI_passthrough_via_OVMF#Ensuring_that_the_groups_are_valid):

```
$ shopt -s nullglob
for g in $(find /sys/kernel/iommu_groups/* -maxdepth 0 -type d | sort -V); do
    echo "IOMMU Group ${g##*/}:"
    for d in $g/devices/*; do
        echo -e "\t$(lspci -nns ${d##*/})"
    done;
done;

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
[...]
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
[...]
```

In the above example, most devices are well isolated, at the exception to  the USB controller and the HD audio controller. 

> In general, but not always, devices associated to a particular IOMMU group have to be passed through a guest system together
{.is-info}


As Phyllome OS is installed on the Intel SSD 660P NVMe SSD, this device should not be shared with a guest system.

| IOMMU Group | Bus | Device | ID  | 
| --- | --- | --- | --- |
| 0   | 0x3d | Intel Corporation Iris Pro Graphics 580 | 8086:193b |
| 2   | | Intel Gaussian Mixture Model - Neural Network Accelerator | 8086:1911 |
| **3**   | | USB 3.0 xHCI Controller | 8086:a12f |
| **3**   | | Thermal Subsystem | 8086:a131 |
| 4   | | MEI Controller | 8086:a13a |
| **11**  | | HM170 Chipset LPC/eSPI Controller | 8086:a14e |
| **11**  | | Power Management Controller | 8086:a121 |
| **11**  | | HD Audio Controller | 8086:a170 |
| **11**  | 0x1f | SMBus | 8086:a123 |
| 12  | 0x1d | Ethernet Connection I219-LM | 8086:15b7 |
| 13  | 0x02 | SD/MMC Card Reader Controller | 1217:8621 |
| 14  | 0x03 | Intel Corporation Wireless 8260 | 8086:24f3 |
| 15  | 0x3d | NVMe SSD Controller SM951/PM951 | 144d:a802 |
| 16  | 0x3e | Intel Corporation SSD 660P Series | 8086:f1a8 |

```
  <hostdev mode="subsystem" type="pci" managed="yes">
      <source>
        <address domain="0x0000" bus="0x03" slot="0x00" function="0x0"/>
      </source>
      <address type="pci" domain="0x0000" bus="0x09" slot="0x00" function="0x0"/>
    </hostdev>
    <hostdev mode="subsystem" type="pci" managed="yes">
      <source>
        <address domain="0x0000" bus="0x02" slot="0x00" function="0x0"/>
      </source>
      <address type="pci" domain="0x0000" bus="0x0a" slot="0x00" function="0x0"/>
    </hostdev>
    <hostdev mode="subsystem" type="pci" managed="yes">
      <source>
        <address domain="0x0000" bus="0x00" slot="0x08" function="0x0"/>
      </source>
      <address type="pci" domain="0x0000" bus="0x10" slot="0x01" function="0x0"/>
    </hostdev>
    <hostdev mode="subsystem" type="pci" managed="yes">
      <source>
        <address domain="0x0000" bus="0x3d" slot="0x00" function="0x0"/>
      </source>
      <address type="pci" domain="0x0000" bus="0x0c" slot="0x00" function="0x0"/>
    </hostdev>
```

- Let's have a look inside the guest system that has the physical devices attached to it:

```
$ lspci
00:00.0 Host bridge: Intel Corporation 82G33/G31/P35/P31 Express DRAM Controller
00:01.0 VGA compatible controller: Red Hat, Inc. Virtio 1.0 GPU (rev 01)
00:02.0 PCI bridge: Red Hat, Inc. QEMU PCIe Root port
[...]
00:1f.0 ISA bridge: Intel Corporation 82801IB (ICH9) LPC Interface Controller (rev 02)
00:1f.2 SATA controller: Intel Corporation 82801IR/IO/IH (ICH9R/DO/DH) 6 port SATA Controller [AHCI mode] (rev 02)
[...]
09:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
0a:00.0 SD Host controller: O2 Micro, Inc. SD/MMC Card Reader Controller (rev 01)
0b:00.0 PCI bridge: Red Hat, Inc. Device 000e
0c:01.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model
0d:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM951/PM951 (rev 01)
``` 

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