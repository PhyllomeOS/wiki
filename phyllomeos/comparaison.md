---
title: Comparaison
description: 
published: true
date: 2022-01-18T09:59:01.609Z
tags: 
editor: markdown
dateCreated: 2022-01-07T10:39:15.878Z
---

# Comparaison

Phyllome OS draws inspiration from numerous other projects, including desktop-oriented systems such as [Qubes OS](https://www.qubes-os.org/), [Tails](https://tails.boum.org/), and [Fedora Silverblue](https://silverblue.fedoraproject.org/), as well as others specialized in running container workloads, such as [Fedora CoreOS](https://silverblue.fedoraproject.org/) and [RancherOS](https://rancher.com/).

When it comes to virtualization-friendly, open-source, desktop-oriented operating systems, two projects stand out: Qubes OS and [Spectrum](https://spectrum-os.org/). How do they compare to Phyllome OS?

## Qubes OS

Like Phyllome OS, Qubes OS is based on Fedora but relies on Xen, the other popular open-source hypervisor for Linux. 

Xen strongly isolates components of the hardware stack, including the USB and network controllers. By design, it works in parallel rather than alongside Linux, as KVM does. KVM’s more tight integration with the Linux Kernel can be considered an advantage or a disadvantage.

Out of security concerns, Qubes OS does not yet support 3D-accelerated virtual machines, even though its parent project Xen does support this functionality. Phyllome OS intends to support 3D acceleration inside virtual machines, even if it means increasing the attack surface.

## Spectrum

Just as with Qubes OS, Spectrum’s main focus is secure computing. Spectrum uses Nix, a declarative packet manager. It is built atop crosvm and thus doesn’t rely on QEMU, largely reducing the attack surface. Through a re-implementation of the virtio-wayland device, which is used in Chrome OS to securely run Linux apps alongside the main OS, Spectrum will eventually allow its guests’ virtual machines to have a GPU capable of efficiently accelerating 3D applications.

By design, Spectrum won't support operating systems that don't rely on the Wayland protocol.

|  | Qubes OS | Spectrum | Phyllome OS 1.0 | 
| :- | :-: | :-: | 
| *Emulator* | QEMU[^1] | crosvm | Cloud Hypervisor |
| *Hypervisor* | Xen | KVM | KVM |
| *Virtual chipset* | i440fx? / Q35? | ? | virt |
| *Default filesystem* | Ext4? | Ext4? | F2F2 |
| *Non-Linux guests support* | Yes | No | Yes |
| Based on | Fedora | Chromium OS | Fedora CoreOS |
| Desktop Environment | Xfce | Aura? | GNOME Shell/Headless|
| Package management | RPM | Nix | RPM-ostree |
| Rolling release | No | Yes? | Yes |
| Live edition | No | No | Yes |
| OS as the center of the UX | Yes | Yes | No |
| Encryption | dm-crypt | dm-crypt | fscrypt |
| Security-focused | yes | yes | no |

[^1]: Since 2017, Xen, upon which Qubes OS relies, is also exploring the possibility to [avoid using QEMU](https://wiki.xenproject.org/wiki/Xen_Project_Software_Overview#Guest_Types) for guests using hardware-assisted virtualization. See the diagram on the “Guest Types” section:“Xen Project Software Official Overview.”.

From a design perspective, Qubes OS and Spectrum are end-to-end operating systems, whereas Phyllome OS is only a wrapper around the user’s preferred operating system. Thanks to nested-virtualization, it could even be used to host those operating systems, but in this configuration, the attack surface would be significantly increased, and the performance would take a significant hit, especially for nested guests.

In Phyllome OS, the main computing activity will happen inside the user’s virtual machine. In QubesOS, Dom0 (“domain zero”) is at the center of the user’s experience. 

In summary, despite some shared characteristics, Phyllome OS is not meant to be a replacement for Qubes OS or Spectrum, but could become a test bed for these operating systems.

---

*[**Go to parent level**](/phyllomeos/)*