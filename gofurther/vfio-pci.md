---
title: Virtual Function I/O passthrough (vfio-pci)
description: Pass a physical device to a guest sysstem
published: true
date: 2025-04-02T18:18:52.594Z
tags: 
editor: markdown
dateCreated: 2025-04-01T11:18:43.924Z
---

# *Vfio-pci* configuration

[Virtual Function I/O](https://www.kernel.org/doc/html/latest/driver-api/vfio.html) (vfio-pci) passthrough allows for a single physical device to be assigned to a virtual machine or container.


## Preparation

* [Install](/deploy/install) any version of Phyllome OS

* Make sure the GRUB has been updated after the first boot: 
`# grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg`

## How to share a physical device

### Collect information

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

In the above example, most devices are well isolated in their own IOMMU group, at the exception to  the USB controller and the HD audio controller. 

> In general, but not always, devices associated to a particular IOMMU group have to be passed through a guest system together
{.is-info}

In our example, Phyllome OS is installed on the Intel SSD 660P NVMe SSD. This device should *not* be shared with a guest system.

| IOMMU Group | Bus | Slot | Function | Device | ID | 
| --- | --- | --- | --- | --- | --- |
| 0 | 0x00 | 0x02 | 0x0 | Intel Corporation Iris Pro Graphics 580 | 8086:193b |
| 2 | 0x00 | 0x08 | 0x0 | Intel Gaussian Mixture Model - Neural Network Accelerator | 8086:1911 |
| **3**   | 0x00 | 0x14 | 0x0 | USB 3.0 xHCI Controller | 8086:a12f |
| **3**   | 0x00 | 0x14 | 0x2 | Thermal Subsystem | 8086:a131 |
| 4  | 0x00 | 0x16 | 0x0 | MEI Controller | 8086:a13a |
| **11** | 0x00 | 0x1f | 0x0 | M170 Chipset LPC/eSPI Controller | 8086:a14e |
| **11** | 0x00 | 0x1f | 0x2 | Power Management Controller | 8086:a121 |
| **11** | 0x00 | 0x1f | 0x3 | HD Audio Controller | 8086:a170 |
| **11** | 0x00 | 0x1f | 0x4 | SMBus | 8086:a123 |
| 12 | 0x00 | 0x1f | 0x4 | Ethernet Connection I219-LM | 8086:15b7 |
| 13 | 0x02 | 0x00 | 0x0 | SD/MMC Card Reader Controller | 1217:8621 |
| 14 | 0x03 | 0x00 | 0x0 | Intel Corporation Wireless 8260 | 8086:24f3 |
| 15 | 0x3d | 0x00 | 0x0 | NVMe SSD Controller SM951/PM951 | 144d:a802 |

### Example 1: share a wireless controller

Let's focus on sharing the wireless controller, which is conveniently located on a IOMMU group of its own.

```
IOMMU Group 14:
	03:00.0 Network controller [0280]: Intel Corporation Wireless 8260 [8086:24f3] (rev 3a)
```

The first digits corresponds to the bus, slot and function associated to the device.

| IOMMU Group | Bus | Slot | Function | Device | ID | 
| --- | --- | --- | --- | --- | --- |
| 14 | 0x03 | 0x00 | 0x0 | Intel Corporation Wireless 8260 | 8086:24f3 |

In order to share such wireless card with a guest, edit the XML file associated to the domain and add the following:

```
<domain type="kvm">
[...]
	<devices>
[...]
		<hostdev mode="subsystem" type="pci" managed="yes">
  		<source>
    		<address domain="0x0000" bus="0x00" slot="0x14" function="0x0"/>
  		</source>
		</hostdev>
[...]
	</devices>
[...]
</domain>
```

- Start the domain and have a look inside the guest system that has the physical devices attached to it:

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
09:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
``` 

The wireless controller has been successfully attached to bus 9 of the virtual chipset.

### Example 2: share the USB controller

Let's try to share the USB controller, which is in the same IOMMU group as the Thermal Subsystem.

```
IOMMU Group 3:
	00:14.0 USB controller [0c03]: Intel Corporation 100 Series/C230 Series Chipset Family USB 3.0 xHCI Controller [8086:a12f] (rev 31)
	00:14.2 Signal processing controller [1180]: Intel Corporation 100 Series/C230 Series Chipset Family Thermal Subsystem [8086:a131] (rev 31)
```

| IOMMU Group | Bus | Slot | Function | Device | ID | 
| --- | --- | --- | --- | --- | --- |
| **3**   | 0x00 | 0x14 | 0x0 | USB 3.0 xHCI Controller | 8086:a12f |
| **3**   | 0x00 | 0x14 | 0x2 | Thermal Subsystem | 8086:a131 |

The two devices has to be shared with the guest at the same time. Edit the XML file associated to the domain and add the following:

```
<domain type="kvm">
[...]
	<devices>
[...]
    <hostdev mode="subsystem" type="pci" managed="yes">
      <source>
        <address domain="0x0000" bus="0x00" slot="0x14" function="0x0"/>
      </source>
    </hostdev>
    <hostdev mode="subsystem" type="pci" managed="yes">
      <source>
        <address domain="0x0000" bus="0x00" slot="0x14" function="0x2"/>
      </source>
    </hostdev>
 
[...]
	</devices>
[...]
</domain>
```

- Start the domain and have a look inside the guest system that has the physical devices attached to it:

```
$ lspci

00:00.0 Host bridge: Intel Corporation 82G33/G31/P35/P31 Express DRAM Controller
[...]
0b:00.0 PCI bridge: Red Hat, Inc. Device 000e
0c:03.0 USB controller: Intel Corporation 100 Series/C230 Series Chipset Family USB 3.0 xHCI Controller (rev 31)
0c:04.0 Signal processing controller: Intel Corporation 100 Series/C230 Series Chipset Family Thermal Subsystem (rev 31)
``` 

The USB controller and the Thermal Subsystem has been successfully attached to the domain.

- All devices attached to physical USB ports will be automatically shared with the guest system

```
$ lsusb

Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 002: ID 1a40:0101 Terminus Technology Inc. Hub
Bus 001 Device 003: ID 8087:0a2b Intel Corp. Bluetooth wireless interface
Bus 001 Device 004: ID 046d:c077 Logitech, Inc. Mouse
Bus 001 Device 005: ID 046d:c31c Logitech, Inc. Keyboard K120
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
``` 

---

*[**Go to parent page**](https://wiki.phyllo.me/)*