---
title: Post-installation configuration
description: 
published: true
date: 2022-07-30T01:01:25.043Z
tags: 
editor: markdown
dateCreated: 2022-07-30T01:01:25.043Z
---

# Post-installation configuration

After Phyllome OS [has been successfully installed](/deploy/install) and [its first-launch process completed](/deploy/install#first-launch), a few tasks are required before it can be used to its fullest potential.

> As Phyllome OS evolves, the following post-installation configuration will, hopefully, be made obsolete 
{.is-info}

## Perform a global checkup

Before creating your first virtual machine, it is a good idea to check if everything is correctly set up.


The command-line tool `virt-host-validate` allows you to check whether virtualization features are activated or not.

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
  QEMU: Checking for cgroup 'devices' controller support                     : WARN[^1] (Enable 'devices' in kernel Kconfig file or mount/enable cgroup controller in your system)
  QEMU: Checking for cgroup 'blkio' controller support                       : PASS
  QEMU: Checking for device assignment IOMMU support                         : PASS
  QEMU: Checking if IOMMU is enabled by kernel                               : PASS
```

[^1]: The warning message for *cgroup devices* can be disregarded, as it won't show up if the `virt-host-validate` command is executed as *root*. [Related discussion](https://gitlab.com/libvirt/libvirt/-/issues/94).

> *If `/dev/kvm` is not found, please ensure that your hardware [is indeed compatible](/deploy/prepare#meet-the-requirements) and that hardware-assisted virtualization [has been activated](/deploy/prepare#enable-hardware-assisted-virtualization) in the BIOS/EFI.*
{.is-info}

## Specific checkup

### Hardware-assisted virtualization (1st gen)

* For Intel CPUs, you can use the following more specific command to check whether *hardware virtualization* is activated:

```
cat /proc/cpuinfo | grep vmx
```

* For AMD CPUs, the following command can be used:
```
cat /proc/cpuinfo | grep svm
```

* Look for `svm` for AMD-based processors, or `vmx` for Intel-based processors.

```
[groot@phyllome ~]$ cat /proc/cpuinfo | grep svm
flags		: fpu vme de  [...] svm [...] sme sev sev_es
```

### Hardware-assisted virtualization (2st gen, IOMMU-based)

Your computer may be compatible with advanced hardware virtualization features (*AMD Vi* or Intel *VT-d*). 

* Check the presence of IOMMU-based hardware-assisted virtualization using the following command [^2]: 

[^2]: Courtesy of the [Archlinux wiki](https://wiki.archlinux.org/title/PCI_passthrough_via_OVMF#Enabling_IOMMU).

```
dmesg | grep -i -e DMAR -e IOMMU
``` 
* Make sure the result looks like this:
```
[    0.600228] iommu: Default domain type: Translated 
[    0.624416] pci 0000:00:00.2: AMD-Vi: IOMMU performance counters supported
[    0.624444] pci 0000:00:01.0: Adding to iommu group 0
[...]
[    0.624690] pci 0000:0b:00.4: Adding to iommu group 15
[    0.627236] pci 0000:00:00.2: AMD-Vi: Found IOMMU cap 0x40
[    0.627987] perf/amd_iommu: Detected AMD IOMMU #0 (2 banks, 4 counters/bank).
```
* You may also want to learn how well isolated your devices are. To do so, copy and paste the following script[^1] in your terminal:

```
for g in `find /sys/kernel/iommu_groups/* -maxdepth 0 -type d | sort -V`; do
    echo "IOMMU Group ${g##*/}:"
    for d in $g/devices/*; do
        echo -e "\t$(lspci -nns ${d##*/})"
    done;
done;
```

[^1]: Courtesy of the [Archlinux wiki](https://wiki.archlinux.org/title/PCI_passthrough_via_OVMF#Ensuring_that_the_groups_are_valid)

* In the following case, devices are rather poorly isolated. The use of the ACS override patch may be warranted (more on that later...).

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

### Grant the current user the ability to manage system-based virtual machines

Any new user, including the one that has been created during the first-launch set up, won't be part of the `libvirt` group. It  means that it won't be able to manage the *qemu:///system*, which runs `libvirt` as root.

To avoid a password prompt each time you connect to *qemu:///system*, you can add the current user to the `libvirt` by using the following command, in the terminal:

```
sudo usermod -a -G libvirt $(whoami)
```

> Phyllome OS will eventually switch to the *qemu:///session* URI, which doesn't require elevated privileges. Have a look at [this great blog post](https://blog.wikichoon.com/2016/01/qemusystem-vs-qemusession.html) to understand some of the differences between the *session* and the *system* URI.  
{.is-info}

## Update GRUB and reboot

Unfortunately, the GRUB config won't correctly update during the kickstart phase, so it has to be done manually.

```
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```
When the is done, please reboot: `sudo reboot`

---

*Are you looking for tasks to do with your system? If so, have a look at doing some [suggested tasks](/gofurther)*

[^1]: Although, we very much encourage you to [hack it](https://github.com/PhyllomeOS/phyllomeos#how-to-hack-phyllome-os).