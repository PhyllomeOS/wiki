---
title: Machine definition
description: Virtual machine hardware
published: true
date: 2025-06-01T17:41:22.711Z
tags: 
editor: markdown
dateCreated: 2025-06-01T17:37:29.262Z
---

# Virtual machine hardware

Libvirt uses XML files to define virtual machine hardware.

In the context of libvirt, a virtual machine or guest system is called a domain. In turn, a domain type refers to the hypervisor used for running the virtual machine.

## Domain type

At the moment, Phyllome OS focuses solely on hardware-assisted virtualization with [KVM and QEMU](https://www.libvirt.org/drvqemu.html). Therefore, the domain type KVM is the one used by default.

``` 
<domain type='kvm'>
  [...]
</domain>
```

Not all QEMU commands are supported by Libvirt. To [pass QEMU commands](https://www.libvirt.org/drvqemu.html#pass-through-of-arbitrary-qemu-commands
), one need to use the following instead and add the QEMU command line at the end :

```
<domain type='kvm' xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'>
	[...]
  <qemu:commandline>
    <qemu:arg value='-device'/>
    <qemu:arg value='ipmi-bmc-sim,id=bmc0'/>
    <qemu:arg value='-device'/>
    <qemu:arg value='smbus-impi,bmc=bmc0'/>
    <qemu:env name='QEMU_MODULE_DIR' value='/usr/lib64/qemu'/>
  </qemu:commandline>
</domain>
```

> If QEMU command lines are not immediately provided, it will automatically revert to simply `<domain type='kvm'>` upon writing changes to the domain
{.is-info}

Under QEMU, the said domain definition translates to: 

```
qemu-system-x86_64 -enable-kvm [...]
```

