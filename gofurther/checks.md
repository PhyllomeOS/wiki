---
title: Performs a few checks on Phyllome OS
description: 
published: true
date: 2021-11-27T11:19:25.159Z
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

### Check if IOMMU groups have been created are present

## Validate specific features on the host

> Those commands are valid for only specific Phyllome OS editions
{.is-info}