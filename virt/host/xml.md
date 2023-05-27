---
title: XML
description: 
published: true
date: 2021-11-13T12:08:22.579Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:58:34.005Z
---

> Section under construction.
{.is-warning}

# Anatomy of a XML file

## Dump XML description

> **Requirements**: To dump the XML configuration of an existing virtual machine to a file, make sure your current user is part of the *libvirt* group and has access to the said virtual machine. 
{.is-info}

* List virtual machines

```
virsh list --all
```

```
Id   Name                       State
-------------------------------------------
 -   phyllomeos                 shut off
``` 

Any XML configuration associated to a specific virtual machine can be dumped to a file using the following command:

* Dump the XML description of phyllomeos to a file
```
$ virsh dumpxml phyllomeos > phyllomeos.xml 
```
## Description

This is the description of an XML file associated to a virtio-based virtual machine. Only relevant features to Phyllome OS are commented. 

```
<!-- Domain type refers to the kind of hypervisor in use. Instead of only relying on kvm, we add the xmlns:qemu bits, which allow us to extend <domain type='kvm'>, and most notably to add specific qemu-command at the end of the file -->
<domain type='kvm' xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'>

<!-- The name of the virtual machine must be unique. Intendation matters -->
	<name>phyllomeos</name>

<!-- The Universally Unique Identifier (UUID) must be unique (ahem). It can be generated using the uuidgen command line tool. -->
	<uuid>12345678-1234-1234-1234-12345678912</uuid>

<!-- Metada are information on the virtual machine itself, its user-generated description or the kind of operating system it runs  -->
  <metadata>
    <libosinfo:libosinfo xmlns:libosinfo="http://libosinfo.org/xmlns/libvirt/domain/1.0">
      <libosinfo:os id="http://fedoraproject.org/fedora/34"/>
    </libosinfo:libosinfo>
  </metadata>

<!-- Memory allocated to the virtual machine. An upward limit can be set by the "memory" line. If the guest OS supports it, you may set the currentMemory value bellow the memory. -->
  <memory unit='KiB'>4145152</memory>
  <currentMemory unit='KiB'>4145152</currentMemory>

<!-- vcpu assignement can either be dynamic or static -->
  <vcpu placement='static'>2</vcpu>

<!-- Architecture and machine type. Here, an x86-64 PCI-express Q35 based machine is being used -->
	<os>
    <type arch='x86_64' machine='pc-q35-5.2'>hvm</type>
<!-- UEFI-based loader -->
	  <loader readonly='yes' type='pflash'>/usr/share/edk2/ovmf/OVMF_CODE.fd</loader>
    <nvram>/var/lib/libvirt/qemu/nvram/phyllome.fd</nvram>
    <bootmenu enable='no'/>
  </os>

 <!-- Specific features for the machine. It equates to UEFI settings-->
  <features>
    <acpi/>
    <apic/>
    <vmport state='off'/>
    <ioapic driver='qemu'/>
  </features>

 <!-- CPU mode -->
  <cpu mode='host-model' check='partial'/>

 <!-- Insert comment here -->
  <clock offset='utc'>
    <timer name='rtc' tickpolicy='catchup'/>
    <timer name='pit' tickpolicy='delay'/>
    <timer name='hpet' present='no'/>
  </clock>

 <!-- Insert comment here -->
  <on_poweroff>destroy</on_poweroff>
  <on_reboot>restart</on_reboot>
  <on_crash>destroy</on_crash>

<!-- Insert comment here -->
  <pm>
    <suspend-to-mem enabled='no'/>
    <suspend-to-disk enabled='no'/>
  </pm>

<!-- Insert comment here -->
  <devices>
    <emulator>/usr/bin/qemu-system-x86_64</emulator>

<!-- Virtio-based disk image using the raw format -->
    <disk type='file' device='disk'>
      <driver name='qemu' type='raw'/>
      <source file='/var/lib/libvirt/images/phyllome.img'/>
      <target dev='vda' bus='virtio'/>
      <boot order='1'/>
      <address type='pci' domain='0x0000' bus='0x04' slot='0x00' function='0x0'/>
    </disk>

<!-- Emulated USB 3 controller -->
    <controller type='usb' index='0' model='qemu-xhci' ports='15'>
      <address type='pci' domain='0x0000' bus='0x02' slot='0x00' function='0x0'/>
    </controller>

<!-- SCSI controller -->
    <controller type='scsi' index='0'>
      <address type='pci' domain='0x0000' bus='0x00' slot='0x1f' function='0x2'/>
    </controller>

<!-- PCI-root -->
   	<controller type='pci' index='0' model='pcie-root'/>

<!-- PCI-express slots. 8 are created. Only two are shown -->
		<controller type="pci" index="1" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="1" port="0x10"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x02" function="0x0" multifunction="on"/>
    </controller>
    <controller type="pci" index="2" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="2" port="0x11"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x02" function="0x1"/>
    </controller>

<!-- Insert comment here -->
    <controller type='virtio-serial' index='0'>
      <address type='pci' domain='0x0000' bus='0x03' slot='0x00' function='0x0'/>
    </controller>

 <!-- Virtio-based network device using NAT  -->
    <interface type='network'>
      <mac address='52:54:00:6d:5d:e2'/>
      <source network='default'/>
      <model type='virtio'/>
      <address type='pci' domain='0x0000' bus='0x01' slot='0x00' function='0x0'/>
    </interface>

 <!-- Insert comment here -->
    <channel type='unix'>
      <target type='virtio' name='org.qemu.guest_agent.0'/>
      <address type='virtio-serial' controller='0' bus='0' port='1'/>
    </channel>

 <!-- Insert comment here -->
    <channel type='spicevmc'>
      <target type='virtio' name='com.redhat.spice.0'/>
      <address type='virtio-serial' controller='0' bus='0' port='2'/>
    </channel>

 <!-- Legacy PS/2 input mouse input device. Hard-coded on QEMU -->
    <input type='mouse' bus='ps2'/>

 <!-- Legacy PS/2 input mouse input device. Hard-coded on QEMU -->
    <input type='keyboard' bus='ps2'/>

<!-- Virtio-input mouse device -->
    <input type="tablet" bus="virtio">
      <address type="pci" domain="0x0000" bus="0x01" slot="0x00" function="0x0"/>
    </input>

 <!-- Virtio-input keyboard device -->
    <input type="keyboard" bus="virtio">
      <address type="pci" domain="0x0000" bus="0x07" slot="0x00" function="0x0"/>
    </input>
  
 <!-- Output the guest display to Spice, for local use only. Use image compression and OpenGL (Only works with Intel GPUs, perhaps AMD ones too) -->
    <graphics type='spice'>
      <listen type='none'/>
      <image compression="auto_glz"/>
      <jpeg compression="auto"/>
      <zlib compression="auto"/>
      <playback compression="on"/>
			<image compression='off'/>
      <gl enable='yes' rendernode='/dev/dri/by-path/pci-0000:00:02.0-render'/>
    </graphics>

 <!-- Virtio-gpu device with 3D acceleration -->
    <video>
      <model type='virtio' heads='1' primary='yes'>
        <acceleration accel3d='yes'/>
      </model>
      <address type='pci' domain='0x0000' bus='0x00' slot='0x01' function='0x0'/>
    </video>

 <!-- Virtio-based memballoon device, to allow memory to grow dynamically in a virtual machine. For Windows-guests, it is better to turn this feature off -->
    <memballoon model='virtio'>
      <address type='pci' domain='0x0000' bus='0x05' slot='0x00' function='0x0'/>
    </memballoon>

 <!-- Virtio random number generator  -->
    <rng model='virtio'>
      <backend model='random'>/dev/urandom</backend>
      <address type='pci' domain='0x0000' bus='0x06' slot='0x00' function='0x0'/>
    </rng>

<!-- Virtio-iommu device, compatible with AMD and Intel CPUs  -->
     <iommu model='intel'>
       <driver intremap='on' iotlb='on'/>
    </iommu>
<!-- End of device section -->
  </devices>

<!-- Start of qemu:commandline section. Requires <domain type='kvm' xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'> at the beginning of the XML file -->
  <qemu:commandline>
    <qemu:env name="DISPLAY" value=":1"/>
    <qemu:env name="GDK_SCALE" value="1.0"/>
    <qemu:env name='INTEL_DEBUG' value='norbc'/>
    <qemu:arg value='-set'/>
    <qemu:arg value='device.hostdev0.x-igd-opregion=on'/>
    <qemu:arg value="-set"/>
    <qemu:arg value='device.hostdev0.driver=vfio-pci-nohotplug'/>
    <qemu:arg value='-set'/>
    <qemu:arg value='device.hostdev0.ramfb=on'/>
    <qemu:arg value='-set'/>
    <qemu:arg value="device.hostdev0.display=on"/>
    <qemu:arg value='-set'/>
    <qemu:arg value="-display"/>
    <qemu:arg value='-set'/>
    <qemu:arg value="gtk,gl=on"/>
    <qemu:arg value='-set'/>
  </qemu:commandline>

<!-- End of domain section. -->
</domain>
```

## Reference

For a more thorough description, see https://libvirt.org/formatdomain.html

---

*[**Go to parent page**](https://wiki.phyllo.me/)*