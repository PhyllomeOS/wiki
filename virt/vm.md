---
title: Machine definition
description: Virtual machine hardware
published: true
date: 2025-06-02T17:41:18.805Z
tags: 
editor: markdown
dateCreated: 2025-06-01T17:37:29.262Z
---

# Virtual machine hardware

Libvirt uses XML files to define virtual machine hardware.

In the context of libvirt, a virtual machine or guest system is called a domain. 

A domain *type* refers to the hypervisor used for running the virtual machine.

- Truncated snippet of an imaginary virtual machine called *phyllome*:

```
<domain type='kvm'>
  <name>phyllome</name>
  <memory unit="GiB">1</memory>
  <vcpu placement='static'>1</vcpu>
  <os firmware="efi">
  <devices>
    <emulator>/usr/bin/qemu-system-x86_64</emulator>
    <input type='keyboard' bus='virtio'>
    </input>
	</devices>
</domain>
```

One can identify the domain type, KVM, the machine name, *phyllome*, the allocated memory, 1 GiB, the vCPU allocation, 1vCPU, the firmware type, UEFI. 

These elements are primarily managed by Linux and KVM, whereas the elements within the devices section are managed by QEMU. One can find the keyboard, for instance.

## Domain type

At the moment, Phyllome OS focuses solely on hardware-assisted virtualization with [KVM and QEMU](https://www.libvirt.org/drvqemu.html). Therefore, the domain type KVM is the one used by default.

``` 
<domain type='kvm'>
  [...]
</domain>
```

Not all QEMU commands are supported by Libvirt. To [pass QEMU commands](https://www.libvirt.org/drvqemu.html#pass-through-of-arbitrary-qemu-commands), one need to use the following instead and add the QEMU command line at the end :

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

> If QEMU command lines are not immediately provided, it will automatically revert to simply `<domain type='kvm'>` when writing changes to the domain definition
{.is-info}

Under QEMU, the said domain definition translates simply to: 

```
qemu-system-x86_64 -enable-kvm [...]
```

## Memory

There are many ways to allocate memory. For maximum performance, one could reserve memory to virtual machine in such a way that it may not be used by the host or any other virtual machine.

A sane default, which does not maximize performance, is the following:

```
<domain type='kvm'>
[...]
	<memory unit="GiB">4</memory>
  <currentMemory unit="GiB">1</currentMemory>
[...]  
	<devices>
   	<memballoon model="virtio-non-transitional"/>
  </devices>
</domain>
```

Up to 4 GiB of memory is allocated to the virtual machine, with a minimum of 1 GiB. 

A memballon device is defined, which can release memory to the host and other virtual machine in case it is not needed anymore.

```
<domain type='kvm'>
[...]
  <memoryBacking>
   	<source type="memfd"/>
   	<access mode="shared"/>
  </memoryBacking>
[...]
</domain>
```

What is also done is to mark the memory as shared memory, which is necessary for other features to work, like *virtiofs*.