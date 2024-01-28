
# KVM-related virtual machine monitors

The Kernel-based Virtual Machine (KVM) module for Linux can be leveraged by many virtual machine monitors (VMMs) to achieve near native performance.

### QEMU

[QEMU](https://wiki.qemu.org/) is a very popular emulator which can be used alongside to KVM to leverage hardware-assisted acceleration as found in modern CPUs. In this mode, as used as a virtualizer in QEMU lingo, it can run guest code directly on the host CPU. 

### crosvm

crosvm is the Chrome OS Virtual Machine Monitor. It is integrated with the Chromium Operating System

### cloud-hypervisor

### firecracker

## Comparaison

See Joplin note under Phyllome OS

|  | `QEMU` | `crosvm` | `cloud-hypervisor` | 
| :- | :-: | :-: | :-: |
| *Firmware* | [SeaBIOS](/virt/vm/firmware#seabios) / [OVMF](/virt/vm/firmware#ovmf) | [SeaBIOS](/virt/vm/firmware#seabios) / [OVMF](/virt/vm/firmware#ovmf) | Modified [OVMF](/virt/vm/firmware#ovmf) / [RHF](/virt/vm/firmware#rust-hypervisor-firmware)  |
| *PS/2 devices* | **Yes** | **Yes** | No | 
| *USB Controller* | **Yes** | **Yes** | No | 
| *SATA Controller* | No | **Yes** | No |
| *IDE Controller* | **Yes** | No | No |
| *Floppy Controller* | **Yes** | No | No |
| *TPM Support* | No | **Yes** | No? |
| *PCI-Express Bus* | No | **Yes** | **Yes** |
| *PCI Bus* | **Yes** | No? | No? |
| *Virtual Function I/O* | No | **Yes** | **Yes** |


## Resources

QEMU documentation

https://github.com/firecracker-microvm/firecracker/blob/main/docs/vsock.md


https://github.com/firecracker-microvm/firecracker/blob/main/docs/design.md

---

*[**Go to parent page**](https://wiki.phyllo.me/)*