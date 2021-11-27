---
title: Performs a few checks on Phyllome OS
description: 
published: true
date: 2021-11-27T11:38:00.341Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:39:13.790Z
---

# Check your system

Before diving further, it is a good idea to check if everything has been set-up correctly. 

## Validate generic features on the host

> Those commands are valid for each and every Phyllome OS editions
{.is-info}

### Perform a global check 

The command-line tool `virt-host-validate` can let you quickly check if hardware virtualization is activated, among other features. 

* Use the following command to check your system:
``` 
virt-host-validate
```

* Make sure the result look like this:

```
[groot@phyllome ~]$ virt-host-validate
  QEMU: Checking for hardware virtualization                                 : PASS
  QEMU: Checking if device /dev/kvm exists                                   : PASS
  QEMU: Checking if device /dev/kvm is accessible                            : PASS
  QEMU: Checking if device /dev/vhost-net exists                             : PASS
  QEMU: Checking if device /dev/net/tun exists                               : PASS
  QEMU: Checking for cgroup 'cpu' controller support                         : PASS
  QEMU: Checking for cgroup 'cpuacct' controller support                     : PASS
  QEMU: Checking for cgroup 'cpuset' controller support                      : PASS
  QEMU: Checking for cgroup 'memory' controller support                      : PASS
  QEMU: Checking for cgroup 'devices' controller support                     : WARN (Enable 'devices' in kernel Kconfig file or mount/enable cgroup controller in your system)
  QEMU: Checking for cgroup 'blkio' controller support                       : PASS
  QEMU: Checking for device assignment IOMMU support                         : PASS
  QEMU: Checking if IOMMU is enabled by kernel                               : PASS
```

> The warning message for *cgroup devices* can be disregarded. This is a [not an issue](https://gitlab.com/libvirt/libvirt/-/issues/94). This warning will not show up if the `virt-host-validate` command is executed as *root* or with a user with sudo privileges
{.is-info}

### Check for hardware virtualization

* Another more generic way to check whether *hardware virtualization* is activated or not is the following command:

```
cat /proc/cpuinfo | grep svm '(vmx|svm)'
```

* Look for `svm` for AMD-based processors, or `vmx` for Intel-based processors.

```
[groot@phyllome ~]$ cat /proc/cpuinfo | grep svm '(vmx|svm)'
flags		: fpu vme de  [...] svm [...] sme sev sev_es
```

## Validate specific features on the host

> Those commands are valid for only specific Phyllome OS editions
{.is-info}

### IOMMU-related checks

If your computer ships with advanced hardware virtualization features (*AMD Vi* or Intel *VT-d*), Phyllome OS should have automatically activated them. 

* Verify if that is the case by using the following command, courtesy of the [Archlinux wiki](https://wiki.archlinux.org/title/PCI_passthrough_via_OVMF#Enabling_IOMMU). 

```
dmesg | grep -i -e DMAR -e IOMMU
``` 
* Make sure the result look like this:
```
[    0.600228] iommu: Default domain type: Translated 
[    0.624416] pci 0000:00:00.2: AMD-Vi: IOMMU performance counters supported
[    0.624444] pci 0000:00:01.0: Adding to iommu group 0
[...]
[    0.624690] pci 0000:0b:00.4: Adding to iommu group 15
[    0.627236] pci 0000:00:00.2: AMD-Vi: Found IOMMU cap 0x40
[    0.627987] perf/amd_iommu: Detected AMD IOMMU #0 (2 banks, 4 counters/bank).
```
* You may also want to learn how isolated your devices are. To do that, use the following script, courtesy of the [Archlinux wiki](https://wiki.archlinux.org/title/PCI_passthrough_via_OVMF#Ensuring_that_the_groups_are_valid):

```
#!/bin/bash
shopt -s nullglob
for g in `find /sys/kernel/iommu_groups/* -maxdepth 0 -type d | sort -V`; do
    echo "IOMMU Group ${g##*/}:"
    for d in $g/devices/*; do
        echo -e "\t$(lspci -nns ${d##*/})"
    done;
done;
```

```
IOMMU Group 0:
[...]
01:00.0 Non-Volatile memory controller [0108]: Intel Corporation SSD 660P Series [8086:f1a8] (rev 03)
	02:00.0 USB controller [0c03]: Advanced Micro Devices, Inc. [AMD] Device [1022:43ee]
	02:00.1 SATA controller [0106]: Advanced Micro Devices, Inc. [AMD] Device [1022:43eb]
[...]
	04:00.0 VGA compatible controller [0300]: NVIDIA Corporation GM107 [GeForce GTX 750] [10de:1381] (rev a2)
	04:00.1 Audio device [0403]: NVIDIA Corporation GM107 High Definition Audio Controller [GeForce 940MX] [10de:0fbc] (rev a1)
	07:00.0 Ethernet controller [0200]: Realtek Semiconductor Co., Ltd. RTL8125 2.5GbE Controller [10ec:8125] (rev 05)
IOMMU Group 1:
[...]
09:00.0 VGA compatible controller [0300]: NVIDIA Corporation GM204 [GeForce GTX 970] [10de:13c2] (rev a1)
	09:00.1 Audio device [0403]: NVIDIA Corporation GM204 High Definition Audio Controller [10de:0fbb] (rev a1)
[...]
IOMMU Group 14:
	0b:00.3 USB controller [0c03]: Advanced Micro Devices, Inc. [AMD] Matisse USB 3.0 Host Controller [1022:149c]
IOMMU Group 15:
	0b:00.4 Audio device [0403]: Advanced Micro Devices, Inc. [AMD] Starship/Matisse HD Audio Controller [1022:1487]
```
