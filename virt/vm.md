---
title: Machine definition
description: Virtual machine hardware
published: true
date: 2025-06-19T18:55:10.146Z
tags: 
editor: markdown
dateCreated: 2025-06-01T17:37:29.262Z
---

# Virtual machine hardware

*Libvirt* uses XML files to define virtual machine hardware, from the system firmware to devices like mouse and keyboard.  

In the context of *libvirt*, a virtual machine or guest system is called a domain. 

A domain *type* refers to the hypervisor used for running the virtual machine.

- Truncated snippet of a virtual machine definition:

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

In this snippet, one can identify the domain type, *KVM*, the machine name, *phyllome*, the allocated memory, *1 GiB*, the vCPU allocation, *1 vCPU*, the firmware type, *UEFI*. 

These elements are primarily managed by Linux and KVM, whereas the elements within the devices section are managed by QEMU, as shown by the emulator line. One can find the keyboard in the device section.

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
qemu-system-x86_64 -enable-kvm
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
[...]
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

## (v)CPU

There are multiple XML elements related to the (v)CPU, with many parameters for each of them.

The CPU allocation section defines the number of vCPU associated to the virtual machine. This number cannot exceed the total number of logical CPUs available in the host machine as well as the maximum number of that the KVM hypervisor can assign to a guest. 

The number of logical CPUs is the number of physical cores multiply by the number of threads per core.

- In the following snippet, 4vCPU is assigned to the virtual machine:

```
<domain type='kvm'>
[...]
  <vcpu placement='static'>4</vcpu>
[...]
</domain>
```  

- Another very important element is the CPU mode:

```
<domain type='kvm'>
[...]
	<cpu mode='host-model'>
		<topology sockets="1" dies="1" cores="2" threads="2"/>
  </cpu>
[...]
</domain>
```

The `host-model` mode is not as fast as `host-passthrough` but should allow a guest to be migrated to a host running different hardware, which `host-passthrough` does not. 

In short: it offers a good balance between performance and functionality.

The topology describes the number of sockets, dies, cores and threads. The total number of cores and threads, in particular, has to match the CPU allocation described above. In our example, a total of four logical cores allocated, which translates to two cores each running two threads.

## System firmware and chipset

Phyllome OS primarily focuses on running modern guest operating systems, which often expect UEFI firmware, PCI Express and Secure Boot to be enabled.

- The main definition focused on defining a UEFI firmware based on [TianoCore](https://www.tianocore.org/), an x86_64 architecture running with a q35 chipset. Secure Boot is not yet enabled by default. The default boot device is the CD-ROM  

```
<domain type='kvm'>
[...]
  <os firmware="efi">
    <type arch="x86_64" machine="q35">hvm</type>
    <loader secure='no'/>
    <boot dev="cdrom"/>
  </os>
[...]
</domain>
```

## Hypervisor features

Some extra features can be enabled depending on the guest. 

### For Unix guests

When it comes to modern Linux guests, only a few features are enabled in the context of the default virtual machine definition.

```
<domain type='kvm'>
[...]
  <features>
    <acpi/>
    <apic/>
  </features>
[...]
</domain>
```

ACPI deals with power management, and allow for graceful shutdown to work.

### For Windows NT guests

For Windows NT guests, more features are enabled:

```
<domain type='kvm'>
[...]
  <hyperv mode='custom'>
    <relaxed state='on'/>
    <vapic state='on'/>
    <spinlocks state='on' retries='4096'/>
    <vpindex state='on'/>
    <runtime state='on'/>
    <synic state='on'/>
    <stimer state='on'>
      <direct state='on'/>
    </stimer>
    <reset state='on'/>
    <frequencies state='on'/>
    <reenlightenment state='on'/>
    <tlbflush state='on'>
      <direct state='on'/>
      <extended state='on'/>
    </tlbflush>
  </hyperv>
  [...]
</domain>
```

## The clock

In most case, the guest clock derives from the host clock. 

In the following example, the hardware clock uses [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time), the *KVM clock*, which does *not* a catchup policy :

```
<domain type='kvm'>
[...]
  <clock offset='utc'>
    <timer name='kvmclock'/>
  </clock>
[...]
</domain>
```

> On non realtime kernel, the KVM clock is updated every 5 minutes for all vCPUs, which may not be enough for accurate timekeeping. For that reason, "[Red Hat recommends running NTP in the virtual machine if accurate timekeeping is required](https://access.redhat.com/solutions/27865)"
{.is-info}

### Resources about timekeeping

- Linux Kernel documentation: [Timekeeping Virtualization for X86-Based Architectures](https://docs.kernel.org/virt/kvm/x86/timekeeping.html)
- SUSE documentation: [VM Guest clock settings](https://documentation.suse.com/sles/15-SP3/html/SLES-all/sec-kvm-managing-clock.html#)
- [Best practices for accurate timekeeping for Red Hat Enterprise Linux running on Red Hat Virtualization](https://access.redhat.com/solutions/27865)

## Events configuration

This define section defines action when guest OS triggers a lifecycle operation.

```
<domain type='kvm'>
[...]
  <on_poweroff>destroy</on_poweroff>
  <on_reboot>restart</on_reboot>
  <on_crash>destroy</on_crash>
[...]
</domain>
```

Despite its scary name, the `destroy` means that the domain will be terminated completely and all associated resources released, not that the domain will be erased. 

### Resources about events configuration

- [Events configuration on libvirt website](https://libvirt.org/formatdomain.html#events-configuration)

## Power Management

This define section defines ACPI sleep states, suspend to memory meaning S3 state and suspend to disk S4 state.

```
<domain type='kvm'>
[...]
	<pm>
  	<suspend-to-disk enabled='no'/>
  	<suspend-to-mem enabled='yes'/>
	</pm>
[...]
</domain>
```

> Suspend to memory won't work if a host device like a graphic card is attached to the guest virtual machine
{.is-warning}

### Resources about Power Management

- [Power Management section on libvirt website](https://libvirt.org/formatdomain.html#power-management)

